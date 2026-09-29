# Power BI, DAX e Power Query

## Vocabulário do negócio

Todo domínio comercial tem seu próprio glossário de indicadores e dimensões (ex: receita, volume, ticket médio, meta, share, variação dia a dia/semana a semana, período, segmento, canal, região).

Use os nomes já estabelecidos no negócio. Não invente sinônimo nem traduza o que já tem nome consolidado — isso é o que faz uma medida DAX ou uma coluna fazer sentido pra quem lê o relatório depois.

## DAX

Sempre diga onde a medida vai ser criada e como usar. Fórmula solta sem contexto não é entrega.

Padrão de escrita:

```dax
Ticket Medio =
VAR ReceitaTotal = SUM( fVendas[VENDA] )
VAR VolumeTotal = SUM( fVendas[VOLUME] )
RETURN
    DIVIDE( ReceitaTotal, VolumeTotal )
```

Regras que importam:

- `DIVIDE` em vez de `/`, sempre. Divisão por zero em visual com muitos segmentos aparece como erro na cara do usuário.
- `VAR` pra deixar a intenção legível e evitar recalcular a mesma coisa.
- Contexto de filtro é o centro de tudo: explique por que a medida funciona, não só o que ela faz.
- Escolha consciente entre `ALL`, `ALLSELECTED`, `REMOVEFILTERS` e `KEEPFILTERS` — share e participação dependem exatamente disso, e é onde o total geral costuma sair errado.
- Tabela calendário marcada como tabela de datas antes de qualquer inteligência temporal.
- Confira o total da linha de totais. Medida que soma certo por linha e erra no total é sintoma de granularidade ou de iterador faltando.
- Explique a diferença entre coluna calculada e medida quando a escolha entre as duas for o ponto do problema.

Cuidado com filtro bidirecional e com relacionamento em granularidade diferente da fato — os dois produzem número plausível e errado.

## Power Query M

Nome de etapa claro e descritivo. Etapa redundante removida. Tipagem correta e explícita no fim.

Considere sempre: carregamento por pasta, mudança de estrutura no arquivo de origem, arquivo temporário do Excel (`~$`), aba ausente, coluna ausente, arquivo corrompido, expansão dinâmica de colunas.

`Table.Buffer` só quando houver motivo real. Ele materializa em memória e costuma piorar mais do que ajuda.

Armadilhas comuns em bases corporativas:

- CSV corporativo brasileiro vem com ponto e vírgula, não vírgula
- `NestedJoin` sobre chave não distinta duplica linha; aplique `Table.Distinct` na tabela de lookup antes
- Lookup de apoio muda de posição de coluna entre versões do arquivo; referencie por nome, não por índice

Ao entregar código M, diga onde colar: Editor do Power Query, Página Inicial, Editor Avançado, na consulta X.

## Entrega

Não entregue só a fórmula. Diga onde criar, como usar, o que verificar depois e qual visual deve mudar. E quando o modelo for a causa do problema, aponte o modelo em vez de remendar a medida.
