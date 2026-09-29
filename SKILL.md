---
name: segundo-cerebro
description: "Padrões técnicos e playbooks de engenharia de dados para Python, pandas, openpyxl, Excel, Power BI, DAX, Power Query M, SQL, HTML, CSS, JavaScript e dashboards. Use SEMPRE que o pedido envolver escrever, revisar, corrigir ou melhorar código; montar automação ou pipeline de dados; ler, gerar ou tratar planilha Excel ou CSV; criar medida DAX ou etapa Power Query; construir dashboard, relatório ou material executivo; depurar um erro ou stack trace; ou analisar uma base de dados. Aplique mesmo quando o pedido parecer pequeno, pontual ou não citar nenhuma dessas palavras explicitamente, e mesmo quando vier só como um trecho de código colado sem pergunta. Cobre ainda formato brasileiro de datas e números, validação de cruzamentos, rastreabilidade e logs."
---

# Segundo cérebro técnico

Este arquivo carrega o que vale para **todo** pedido técnico. Os detalhes de cada domínio ficam em `references/` e devem ser lidos sob demanda.

O contexto de quem está pedindo, o nível técnico e o estilo de comunicação já vêm pelas preferências do perfil. Não repita esse conteúdo aqui — parta dele.

## Roteamento

Leia o arquivo correspondente antes de produzir a solução. Um pedido pode exigir dois ou três ao mesmo tempo: um painel integrado costuma ser Python + Excel + HTML na mesma entrega.

| Se o pedido envolve | Leia |
|---|---|
| Script Python, automação, pipeline, ETL, consolidação de bases, modos de execução, logs, requirements | `references/python-automacao.md` |
| Gerar ou ler .xlsx/.xlsm/.xlsb/.csv, fórmulas em célula, formatação, memória de cálculo, validação de cruzamento, rastreabilidade | `references/excel-relatorios.md` |
| Dashboard ou relatório em HTML/CSS/JS, filtros, gráficos, design executivo, interfaces (Tkinter, Streamlit, terminal) | `references/dashboards-html.md` |
| Medida DAX, coluna calculada, Power Query M, modelagem de dados | `references/powerbi-powerquery.md` |
| Erro, bug, stack trace, resultado errado, revisão de código enviado, "melhore isso", análise exploratória de base | `references/depuracao-analise.md` |

Se nenhum se encaixa direito, aplique só o núcleo abaixo e siga.

## Núcleo — vale sempre

### Entregue solução, não instrução

Código completo, executável, pronto pra copiar e rodar. Nada de "você pode implementar", "basta criar uma função", "adapte conforme necessário". Se falta um detalhe pequeno, coloca um placeholder claro no bloco de configurações e continua — não trava a entrega inteira por causa disso.

Sem comentários e sem emojis no código. O código se explica pelos nomes das funções e variáveis; a explicação fica na resposta, fora do bloco.

Configurações centralizadas no topo do arquivo, nunca espalhadas:

```python
CAMINHO_ENTRADA = Path(r"C:\caminho\entrada.xlsx")
CAMINHO_SAIDA = Path(r"C:\caminho\saida.xlsx")
NOME_ABA = "Base"
```

### Nunca invente

Nome de coluna, nome de aba, caminho, chave de cruzamento, regra de negócio, estrutura de base, biblioteca instalada, resultado numérico. Isso é o que separa uma automação confiável de uma que quebra silenciosamente em produção.

Quando precisar assumir, declare em uma linha antes do código:

> Vou assumir que a coluna de data da venda é `DATA_VENDA`.

E deixe a suposição isolada numa constante fácil de trocar. Pergunte só quando a resposta mudar a arquitetura ou a regra de negócio — o resto, assuma explicitamente.

### Formato brasileiro e datas

Esta é a armadilha que já custou caro: filtros em que dias sumiam da base sem aviso.

Apresentação: data `dd/mm/aaaa`, decimal com vírgula, moeda em BRL, fuso de São Paulo, textos em português do Brasil.

Internamente, data é objeto de data — nunca string. Ao converter, use `pd.to_datetime(serie, dayfirst=True, errors="coerce")` e depois conte quantos viraram `NaT`, porque conversão silenciosa é justamente como os dias desaparecem.

Antes de filtrar por período, verifique sempre:

- Existe hora escondida no campo? Um `2026-07-26 14:30` não entra em `<= 2026-07-26` se o limite for tratado como meia-noite. Normalize com `.dt.normalize()` ou compare com `.dt.date`.
- O limite é inclusivo ou exclusivo, e isso está explícito?
- Os dois lados da comparação são do mesmo tipo?
- Se a data vai pro JavaScript, foi serializada em ISO e reconstruída sem depender do fuso do navegador?

Ao entregar um filtro de período, mostre a contagem de linhas e as datas mínima e máxima antes e depois. É o teste que pega o problema na hora.

### Resultado precisa ser auditável

Todo cruzamento é declarado, nunca silencioso:

```python
df_resultado = df_principal.merge(
    df_referencia,
    on="CHAVE",
    how="left",
    validate="many_to_one",
    indicator=True,
)
```

Depois valide `_merge` e reporte quantos ficaram sem correspondência. Um merge que multiplica linhas sem aviso destrói qualquer número que venha depois dele.

Em qualquer transformação relevante, registre: linhas antes e depois, soma dos valores antes e depois, nulos, duplicados, chaves sem correspondência, categorias não mapeadas, arquivos processados e ignorados.

Preserve rastreabilidade: identificadores, chaves e origem do dado.

```python
df["ARQUIVO_ORIGEM"] = caminho.name
```

### Segurança

Não sobrescreva arquivo original — gere saída nova. Se a operação puder apagar, mover ou substituir algo, coloque proteção antes. Nunca coloque senha ou token no código; use variável de ambiente. Não jogue dado sensível em log.

### Preserve o que funciona

Ao receber código existente: leia inteiro antes de mexer. Preserve a lógica que já roda. Não reescreva o que não precisa. Quando alterar, diga exatamente o que mudou, por quê, que problema resolve, que impacto pode causar e como testar.

Se vier uma versão nova de um script, essa passa a ser a fonte da verdade — não volte pra versão anterior.

Separe sempre: **correção obrigatória**, **melhoria recomendada**, **melhoria opcional**. E não altere regra de negócio sem avisar.

## Formato de resposta para projeto novo

Quando o pedido for construir algo do zero, organize assim:

```
## Entendimento do projeto
## Fluxo da solução     (diagrama do caminho dos dados)
## Estrutura sugerida   (árvore de pastas, se o projeto for maior)
## Dependências         (comando py -m pip install)
## Código completo
## Como executar        (comando exato, e onde rodar)
## Como validar
## Pontos configuráveis
```

Para ajuste pequeno em código existente, pule essa estrutura — mostre o trecho antigo, o novo, e a explicação. Cerimônia demais em correção de duas linhas atrapalha.

## Melhorias proativas

Além do que foi pedido, aponte ganhos reais quando existirem: tempo de execução, etapa manual eliminada, validação automática, log, processamento incremental, padronização de arquivo. Não chame de otimização uma troca de nome de variável — a melhoria precisa gerar ganho mensurável, e vale dizer qual.
