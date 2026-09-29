# Python, automações e pipelines

## Ambiente alvo

Windows 10/11, Python 3.14 instalado localmente, VS Code, execução por CMD ou PowerShell. Arquivos em pastas locais, corporativas, OneDrive ou SharePoint.

Comando de instalação sempre nesse formato, e diga onde rodar:

```bash
py -m pip install pandas openpyxl
```

Antes de entregar, considere as falhas típicas desse ambiente: biblioteca instalada em outro interpretador, caminho com espaço, barra invertida engolida por escape, arquivo aberto no Excel travando a escrita, pasta sincronizada com lock, permissão negada, encoding de CSV, separador decimal com vírgula.

Caminho sempre com raw string e `pathlib`:

```python
CAMINHO = Path(r"C:\Users\usuario\Documentos\base.xlsx")
```

## Estrutura padrão

Para automação de porte médio ou maior:

```python
from pathlib import Path
import logging
import pandas as pd


# ============================================================
# CONFIGURAÇÕES
# ============================================================

CAMINHO_ENTRADA = Path(r"C:\caminho\entrada.xlsx")
CAMINHO_SAIDA = Path(r"C:\caminho\saida.xlsx")

COLUNAS_OBRIGATORIAS = ["DATA", "AGENCIA", "SEGMENTO", "VENDA"]


# ============================================================
# FUNÇÕES
# ============================================================

def carregar_dados(caminho: Path) -> pd.DataFrame:
    ...


def validar_colunas(df: pd.DataFrame, obrigatorias: list[str]) -> None:
    ...


def tratar_dados(df: pd.DataFrame) -> pd.DataFrame:
    ...


def salvar_resultado(df: pd.DataFrame, caminho: Path) -> None:
    ...


# ============================================================
# EXECUÇÃO PRINCIPAL
# ============================================================

def main() -> None:
    try:
        df = carregar_dados(CAMINHO_ENTRADA)
        validar_colunas(df, COLUNAS_OBRIGATORIAS)
        df = tratar_dados(df)
        salvar_resultado(df, CAMINHO_SAIDA)
        logging.info("Processo concluído com sucesso.")
    except Exception:
        logging.exception("Erro durante a execução.")
        raise


if __name__ == "__main__":
    main()
```

Script pequeno não precisa disso. Não imponha a cerimônia onde ela só atrapalha.

Projeto grande separa configuração da lógica:

```
projeto/
├── main.py
├── config.py
├── requirements.txt
├── src/
│   ├── leitura.py
│   ├── tratamento.py
│   ├── validacao.py
│   └── exportacao.py
├── entrada/
├── saida/
└── logs/
```

## Qualidade

Type hints em todas as funções. Nomes de função e variável em português quando o projeto está em português — não misture sem necessidade; biblioteca e termo técnico continuam em inglês.

Nunca `except: pass`. Nunca esconder erro relevante. Sempre validar existência de arquivo e de coluna antes de usar.

Trate como padrão, não como exceção: nulos, duplicados, tipo errado, número guardado como texto, espaço extra no nome da coluna, acento, arquivo vazio, arquivo corrompido, planilha aberta.

## Desempenho

O volume real aqui passa de 900 mil linhas e 130 colunas. Isso muda as escolhas.

Evite loop linha a linha. Prefira vetorização: `merge`, `groupby`, `pivot_table`, `map`, `transform`, máscara booleana. Não use `.apply()` por reflexo — ele é loop disfarçado.

Leia só as colunas necessárias (`usecols`). Use chunks quando o arquivo não couber confortavelmente na memória. Libere objeto grande quando não for mais usado.

Quando pandas e openpyxl não derem conta, considere Polars, DuckDB, Parquet, PyArrow, SQLite, processamento incremental ou divisão por período — mas explique o ganho concreto antes de recomendar. Tecnologia mais complexa sem benefício claro é custo de manutenção jogado no colo de quem for manter o código.

Quando o volume for grande, diga qual é o impacto de desempenho da solução entregue.

## Modos de execução

Automação que roda por semana, por período, por país ou por mercado precisa de modo explícito e validado:

```python
MODO_EXECUCAO = "semanal"

MODOS_VALIDOS = {"semanal", "multiplas_semanas", "anual"}

if MODO_EXECUCAO not in MODOS_VALIDOS:
    raise ValueError(f"Modo inválido: {MODO_EXECUCAO}. Use um de {sorted(MODOS_VALIDOS)}.")
```

Assuma sempre que o processo vai rodar de novo com arquivos novos. Solução descartável só se justifica quando reaproveitar for realmente impossível.

## Logs e auditoria

Em automação relevante, registre início, término, tempo de execução, arquivos encontrados, processados e com erro, linhas e colunas, avisos, erros e caminho do arquivo gerado. Quando fizer sentido, gere também um relatório de processamento em Excel ou CSV.

## Testes

Validação simples embutida já resolve a maior parte:

```python
def validar_resultado(df: pd.DataFrame) -> None:
    if df.empty:
        raise ValueError("O resultado ficou vazio.")

    if "VENDA" not in df.columns:
        raise KeyError("A coluna VENDA não foi encontrada.")

    if df["VENDA"].isna().all():
        raise ValueError("A coluna VENDA está completamente vazia.")
```

Projeto maior comporta `pytest`.

## requirements.txt

Inclua quando houver dependência externa. Só o que o código realmente usa. Fixe versão quando a versão importar.

```text
pandas
openpyxl
xlsxwriter
```

## Cabeçalho de documentação

Script grande leva um cabeçalho curto: objetivo, entrada, saída, etapas principais, dependências. Script pequeno não leva documentação nenhuma.
