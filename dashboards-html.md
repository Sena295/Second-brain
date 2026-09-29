# Dashboards, HTML e interfaces

## Antes de codar

Defina, mesmo que rápido: objetivo, público, KPIs prioritários, dimensões, filtros, hierarquia visual, gráficos, tabelas, alertas. Dashboard bonito que não responde à pergunta de negócio não serve.

Público típico aqui é executivo — comitê, diretoria. Isso significa: número principal grande e imediato, comparação com meta, variação e tendência visíveis sem clique.

## Entrega

Arquivo completo, pronto pra abrir no navegador. Projeto pequeno ou médio: tudo num HTML só, mais fácil de mandar por e-mail e abrir em máquina corporativa. Projeto grande: separe CSS e JS.

Sem dependência de build. Sem framework pesado quando CSS e JS puros resolvem.

## Design

Executivo, moderno, limpo, corporativo. Boa hierarquia visual, destaque claro pros KPIs principais, cores semânticas com significado consistente (positivo, negativo, neutro, alerta), espaçamento generoso, tipografia legível em tela de notebook.

Evite: poluição, borda em tudo, cor aleatória, gráfico que não informa, e a mesma informação repetida em vários lugares sem justificativa.

Considere ordem de leitura, contexto temporal, variação absoluta e percentual, ranking, tooltip, drill-down, tabela detalhada e exportação.

Quando for criticar um dashboard existente, mostre como implementar a correção. Crítica sem código não ajuda. E preserve o que já está bom — não transforme o projeto em outra coisa sem justificar.

## Filtros

É onde a maior parte dos bugs mora.

- Filtros precisam ser combináveis, e a opção "Todos" tem que funcionar de verdade
- Gráficos e tabelas leem a mesma base já filtrada, nunca cada um a sua
- O período selecionado fica visível na tela
- Existe botão de limpar filtros
- Valor numérico não é comparado como texto
- Data não é comparada em formatos diferentes

Data em JavaScript merece atenção redobrada. `new Date("2026-07-26")` é interpretado como UTC e, no fuso de São Paulo, volta como dia 25. Compare por string ISO normalizada ou construa a data por componentes:

```javascript
function paraData(texto) {
  const [ano, mes, dia] = texto.split("-").map(Number);
  return new Date(ano, mes - 1, dia);
}
```

Ao serializar do Python pro HTML, mande ISO (`YYYY-MM-DD`) e formate pra `dd/mm/aaaa` só na exibição.

## Estados

Trate carregamento, base vazia, filtro que zerou o resultado e erro. Tela em branco sem explicação é o pior resultado possível para quem está apresentando em reunião.

## Formatação na tela

Número em padrão brasileiro:

```javascript
const formatoBRL = new Intl.NumberFormat("pt-BR", { style: "currency", currency: "BRL" });
const formatoNumero = new Intl.NumberFormat("pt-BR", { maximumFractionDigits: 0 });
```

## Interfaces

Quando ele pedir interface, prefira o mais simples que resolva: terminal, Tkinter, CustomTkinter, Streamlit ou HTML local. A interface existe pra facilitar o uso por quem não tem ambiente de desenvolvimento — normalmente alguém do time rodando um `.bat`.

Ela costuma precisar de: escolher arquivo ou pasta, escolher período, escolher modo de execução, acompanhar progresso, ver mensagem de erro e abrir o arquivo gerado no fim.

Não crie interface só pra parecer sofisticado.
