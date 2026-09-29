# segundo-cerebro-skills

> Skills do Claude que uso no dia a dia para engenharia de dados: Python, Excel, Power BI/DAX/Power Query, dashboards e depuração de código.

Inspirado em repositórios como o [mentor-prompt](https://github.com/guithepc/mentor-prompt), este repositório reúne, de forma pública e reutilizável, algumas das skills do meu "segundo cérebro" — instruções persistentes que carrego para o Claude Code / Claude Skills, para que ele já chegue sabendo como eu gosto que código e análises sejam entregues.

Uma **skill** aqui é um arquivo `SKILL.md` com metadados (`name`, `description`) que o Claude carrega automaticamente quando a descrição bate com o pedido, mais arquivos de referência (`references/*.md`) que só são lidos sob demanda — assim a skill principal fica enxuta e os detalhes de cada domínio não poluem todo pedido.

## O que tem aqui

### [`segundo-cerebro`](skills/segundo-cerebro/SKILL.md)

Playbook técnico para qualquer pedido de código, automação ou análise de dados. Cobre:

| Arquivo | Conteúdo |
|---|---|
| [`SKILL.md`](skills/segundo-cerebro/SKILL.md) | Núcleo: entregar solução completa (não instrução), nunca inventar nome de coluna/regra de negócio, formato de data e número brasileiro, resultado auditável (merges declarados, contagens antes/depois), segurança básica, como reagir a código já existente |
| [`references/python-automacao.md`](skills/segundo-cerebro/references/python-automacao.md) | Padrões para scripts Python, pandas, automação, pipelines, ETL, logs, requirements |
| [`references/excel-relatorios.md`](skills/segundo-cerebro/references/excel-relatorios.md) | Geração e leitura de `.xlsx`/`.csv` com openpyxl, fórmulas, formatação, validação de cruzamento |
| [`references/dashboards-html.md`](skills/segundo-cerebro/references/dashboards-html.md) | Dashboards e relatórios em HTML/CSS/JS, filtros, gráficos, design executivo |
| [`references/powerbi-powerquery.md`](skills/segundo-cerebro/references/powerbi-powerquery.md) | Medidas DAX, colunas calculadas, Power Query M, modelagem |
| [`references/depuracao-analise.md`](skills/segundo-cerebro/references/depuracao-analise.md) | Como depurar bugs, revisar código enviado, analisar bases exploratoriamente |

## Como usar

### Claude Code / Claude Skills

Copie a pasta da skill para o diretório de skills do seu usuário ou projeto:

```bash
cp -r skills/segundo-cerebro ~/.claude/skills/segundo-cerebro
```

O Claude passa a carregar automaticamente o `SKILL.md` quando o pedido combinar com a `description` do frontmatter, e lê os arquivos em `references/` só quando o roteamento interno indicar que são relevantes.

### Como prompt de sistema em qualquer LLM

Cada `SKILL.md`/`references/*.md` também funciona como um bloco de instruções que pode ser colado direto no system prompt de qualquer assistente (ChatGPT, Claude.ai, Gemini etc.) — não depende de nenhuma ferramenta específica.

## Por que publicar isso

Escrever essas regras uma vez e reutilizar evita repetir o mesmo contexto (formato de data, como validar um merge, como entregar uma medida DAX) em toda conversa nova. Publicar aqui serve tanto de backup versionado quanto de ponto de partida pra quem quiser adaptar pro próprio fluxo de trabalho.

Sinta-se à vontade para dar fork e ajustar ao seu domínio e ao seu estilo.

## Licença

[MIT](LICENSE) — use, adapte e distribua livremente.

---

## English

Personal library of Claude Skills I use for day-to-day data engineering work: Python, Excel, Power BI/DAX/Power Query, dashboards, and code review/debugging.

Inspired by repositories like [mentor-prompt](https://github.com/guithepc/mentor-prompt), this repo collects reusable pieces of my "second brain" — persistent instructions I load into Claude Code / Claude Skills so it already knows how I like code and analysis delivered.

A **skill** here is a `SKILL.md` file with frontmatter metadata (`name`, `description`) that Claude auto-loads when a request matches the description, plus `references/*.md` files that are only read on demand — keeping the main skill lean while domain details stay out of the way until needed.

**Included:** [`segundo-cerebro`](skills/segundo-cerebro/SKILL.md) — a technical playbook covering: deliver complete runnable solutions (not instructions), never guess column names/business rules, Brazilian date/number formatting, auditable results (declared merges, before/after row counts), basic security hygiene, and how to handle existing code without breaking what already works. Domain references cover Python automation/ETL, Excel report generation, HTML/JS dashboards, Power BI/DAX/Power Query, and debugging/code review.

To use with Claude Code, copy the skill folder into `~/.claude/skills/`. Since each file is plain Markdown, it also works as a system-prompt block for any LLM.

MIT licensed — fork it and adapt it to your own domain and style.
