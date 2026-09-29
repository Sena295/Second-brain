# Excel, relatórios e validação

## Escolha da biblioteca

Escolha pelo objetivo, não por costume:

| Objetivo | Biblioteca |
|---|---|
| Tratar e analisar dados | pandas |
| Escrever em célula específica, fórmula, formatação, preservar arquivo existente | openpyxl |
| Criar arquivo novo bem formatado do zero | xlsxwriter |
| Ler .xlsb | pyxlsb |
| Interagir com o Excel aberto, recalcular, acionar macro | xlwings |
| Volume que trava o pandas | polars |
| Consulta pesada sobre base grande | duckdb |

Ponto crítico: `pandas.to_excel` reescreve a planilha inteira e destrói fórmulas, formatação e abas que já existiam. Quando o alvo é um arquivo vivo, com abas de apoio e fórmulas, use openpyxl e atualize apenas as células necessárias.

Risco conhecido em atualização cirúrgica: apagar linha com `EntireRow.Delete` derruba tabelas de apoio que moram em colunas laterais da mesma faixa de linhas. Restrinja o escopo às colunas de dados e faça verificação de integridade antes de salvar.

## Padrão do arquivo gerado

Cabeçalho formatado, filtro automático, painel congelado, largura de coluna adequada, data formatada como data, número e percentual com formato correto, abas organizadas, identificação da fonte.

## Fórmulas

Quando ele pedir fórmulas, escreva fórmula na célula. Não substitua tudo por valor já calculado em Python — o ponto é conseguir abrir a planilha e acompanhar de onde o número saiu.

O idioma da fórmula depende do Excel dele. Se ele não informar, diga qual você usou.

Quando o cálculo tiver alguma complexidade, monte uma aba de memória de cálculo com: dados de origem, critérios, fórmulas, chaves de cruzamento, totais, diferenças, validações e explicação curta de cada etapa.

## Validação obrigatória

Relatório tecnicamente executável não basta. O número precisa ser confiável, porque ele vai pra comitê.

Reporte sempre que for relevante:

- linhas antes e depois de cada etapa
- soma dos valores antes e depois
- registros sem correspondência no cruzamento
- duplicados por chave
- nulos em coluna crítica
- data mínima e máxima
- colunas obrigatórias ausentes
- categorias não mapeadas
- arquivos processados e ignorados

Cruzamento sempre declarado:

```python
df_resultado = df_principal.merge(
    df_referencia,
    on="CHAVE",
    how="left",
    validate="many_to_one",
    indicator=True,
)

sem_correspondencia = (df_resultado["_merge"] == "left_only").sum()
if sem_correspondencia:
    logging.warning("Registros sem correspondência: %s", sem_correspondencia)
```

Chave de lookup duplicada multiplica linha e infla total. Antes do merge, verifique se a tabela de referência é única na chave — em Power Query o sintoma é o mesmo com `NestedJoin`.

## Rastreabilidade

Preserve identificadores e chaves na saída. Registre origem: nome do arquivo, nome da aba, período, regra aplicada, o que casou e o que não casou.

```python
df["ARQUIVO_ORIGEM"] = caminho.name
```

O critério prático: dado um número na planilha final, é possível chegar até a linha de origem? Se não, falta coluna.

## Proteção

Gere saída em arquivo novo. Se for realmente necessário substituir, valide o resultado antes e faça backup. Trate `PermissionError` com mensagem clara — quase sempre é o arquivo aberto no Excel, e vale dizer isso na mensagem em vez de deixar o traceback cru.
