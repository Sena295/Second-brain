# Second-Brain

> 68 Skills que uso no dia a dia: engenharia de dados, design de interface, automação, ferramentas de IA local e carreira.

Este repositório reúne, de forma pública e reutilizável, meu "segundo cérebro" de skills e instruções persistentes que carrego para o Claude Code / Claude Skills, para que ele já chegue sabendo como eu gosto que código, design e análises sejam entregues.

Uma **skill** aqui é uma pasta com um arquivo `SKILL.md` (metadados `name` + `description` no frontmatter, e instruções no corpo) que o Claude carrega automaticamente quando o pedido combina com a descrição — mais, em alguns casos, arquivos de referência ou scripts auxiliares que só são lidos sob demanda.
Obsidian tambem é uma boa alternativa para adicionar essas skills 

## Estrutura

```
skills/
├── segundo-cerebro/          # playbook de engenharia de dados (Python, Excel, Power BI, dashboards, debug)
├── design-ui/                # 46 skills — sistema de design, um princípio por skill
├── dev-tools/                # 15 skills — ferramentas de IA local, automação, scraping
├── carreira/                 # 3 skills — automação de busca de emprego
└── produtividade-escrita/    # 2 skills — estilo de escrita e formato de resposta
```

## O que tem aqui

### [`segundo-cerebro`](skills/segundo-cerebro/SKILL.md)

Playbook técnico para qualquer pedido de código, automação ou análise de dados: entregar solução completa (não instrução), nunca inventar nome de coluna/regra de negócio, formato de data e número brasileiro, resultado auditável, segurança básica. Referências para Python/pandas, Excel/openpyxl, dashboards HTML, Power BI/DAX/Power Query e depuração.

### Design & UI (46)

Cada skill cobre **um princípio de design isolado** (cor, tipografia, espaçamento, estado de componente, acessibilidade, motion...), pra poder combinar só o que o projeto precisa em vez de carregar um guia de estilo inteiro toda vez. As `combo-*` empilham 4 delas para um tipo de projeto específico (dashboard, editorial, landing page, MVP).

| Skill | Descrição |
|---|---|
| [`botoes-e-acoes`](skills/design-ui/botoes-e-acoes/SKILL.md) | Define hierarquia de botões e mantém o nome da ação constante do início ao fim do fluxo. |
| [`brief-antes-do-pixel`](skills/design-ui/brief-antes-do-pixel/SKILL.md) | Define público, tom, restrições e diferenciação antes de desenhar ou codar qualquer tela. |
| [`cards-e-listas`](skills/design-ui/cards-e-listas/SKILL.md) | Escolhe entre card, lista e tabela e estrutura cada item com hierarquia interna clara. |
| [`combo-dashboard`](skills/design-ui/combo-dashboard/SKILL.md) | Empilha 4 skills de design para app ou dashboard — grid, estados de componente, contraste e densidade. |
| [`combo-editorial`](skills/design-ui/combo-editorial/SKILL.md) | Empilha 4 skills de design para site de marca ou editorial — voz visual, fontes, imagem e microtipografia. |
| [`combo-landing`](skills/design-ui/combo-landing/SKILL.md) | Empilha 4 skills de design para landing page ou página de produto — elemento assinatura, fontes, cor e hero. |
| [`combo-mvp`](skills/design-ui/combo-mvp/SKILL.md) | Empilha 4 skills de design para MVP rápido — shadcn/ui, tema claro/escuro, espaçamento e microcopy. |
| [`composicao-de-hero`](skills/design-ui/composicao-de-hero/SKILL.md) | Compõe a primeira dobra com o que é mais característico do produto, não o padrão headline + gradiente + botão. |
| [`contraste-acessivel`](skills/design-ui/contraste-acessivel/SKILL.md) | Verifica e corrige contraste de texto, ícones e bordas para WCAG AA em tema claro e escuro. |
| [`contraste-minimo-AA`](skills/design-ui/contraste-minimo-AA/SKILL.md) | Audita uma tela ou paleta contra os mínimos WCAG AA e reporta pares que falham com correção. |
| [`cor-de-acento`](skills/design-ui/cor-de-acento/SKILL.md) | Define e restringe uma única cor de destaque, usada com moderação para guiar a atenção. |
| [`critica-em-2-passos`](skills/design-ui/critica-em-2-passos/SKILL.md) | Planeja tokens, critica o plano contra o brief e só então escreve o código. |
| [`densidade-e-respiro`](skills/design-ui/densidade-e-respiro/SKILL.md) | Calibra whitespace intencional e densidade de informação para telas legíveis. |
| [`easing-e-timing`](skills/design-ui/easing-e-timing/SKILL.md) | Escolhe curvas e durações naturais e as padroniza em tokens de motion. |
| [`elemento-assinatura`](skills/design-ui/elemento-assinatura/SKILL.md) | Escolhe a única coisa memorável de um design e mantém todo o resto quieto. |
| [`escala-tipografica`](skills/design-ui/escala-tipografica/SKILL.md) | Define uma type scale com tamanhos, pesos e tracking em tokens. |
| [`espacamento-consistente`](skills/design-ui/espacamento-consistente/SKILL.md) | Aplica escala de espaçamento baseada em 4/8px, eliminando valores arbitrários. |
| [`estados-de-componente`](skills/design-ui/estados-de-componente/SKILL.md) | Garante que todo componente cubra loading, vazio, erro, parcial e sucesso. |
| [`estados-de-cor`](skills/design-ui/estados-de-cor/SKILL.md) | Deriva cores de hover, active, focus, disabled, selected e erro a partir dos tokens base. |
| [`foco-visivel-por-teclado`](skills/design-ui/foco-visivel-por-teclado/SKILL.md) | Garante focus ring visível e ordem de foco correta para navegação por teclado. |
| [`fontes-com-caractere`](skills/design-ui/fontes-com-caractere/SKILL.md) | Substitui fontes default (Inter, Roboto, system-ui) por famílias com personalidade. |
| [`formularios`](skills/design-ui/formularios/SKILL.md) | Constrói formulários com labels visíveis, validação no momento certo e mensagens claras. |
| [`grid-de-12-colunas`](skills/design-ui/grid-de-12-colunas/SKILL.md) | Estrutura a página num grid de 12 colunas com gutters e container definidos. |
| [`hierarquia-de-titulos`](skills/design-ui/hierarquia-de-titulos/SKILL.md) | Organiza níveis de título (h1–h4, eyebrow, subtítulo) para leitura por varredura. |
| [`hierarquia-visual`](skills/design-ui/hierarquia-visual/SKILL.md) | Define para onde o olho vai primeiro, segundo e terceiro numa tela. |
| [`iconografia-coerente`](skills/design-ui/iconografia-coerente/SKILL.md) | Mantém um só conjunto de ícones com peso, grade e estilo consistentes. |
| [`imagem-e-textura`](skills/design-ui/imagem-e-textura/SKILL.md) | Usa imagens e texturas do universo do assunto em vez de stock genérico. |
| [`logo-e-lockup`](skills/design-ui/logo-e-lockup/SKILL.md) | Define uso, tamanhos mínimos, área de proteção e variações do logo. |
| [`mensagens-de-erro-especificas`](skills/design-ui/mensagens-de-erro-especificas/SKILL.md) | Escreve mensagens de erro que dizem o que houve e o que fazer. |
| [`microcopy-em-voz-ativa`](skills/design-ui/microcopy-em-voz-ativa/SKILL.md) | Escreve rótulos, botões, títulos e mensagens de interface em voz ativa. |
| [`microinteracoes-com-proposito`](skills/design-ui/microinteracoes-com-proposito/SKILL.md) | Adiciona microinterações que confirmam ação ou revelam estado, corta as decorativas. |
| [`microtipografia`](skills/design-ui/microtipografia/SKILL.md) | Corrige aspas curvas, travessões, viúvas, órfãs e ligaduras em texto de interface. |
| [`motion-com-restricao`](skills/design-ui/motion-com-restricao/SKILL.md) | Corta animação excessiva e define um orçamento de movimento para o projeto. |
| [`navegacao`](skills/design-ui/navegacao/SKILL.md) | Estrutura menus e rótulos pelo que o usuário controla, não pela arquitetura interna. |
| [`numeros-tabulares`](skills/design-ui/numeros-tabulares/SKILL.md) | Aplica tabular-nums e formatação correta a tabelas, métricas e preços. |
| [`paleta-por-hue`](skills/design-ui/paleta-por-hue/SKILL.md) | Deriva a paleta inteira de uma cor de marca usando OKLCH. |
| [`pareamento-de-fontes`](skills/design-ui/pareamento-de-fontes/SKILL.md) | Escolhe um par display + corpo deliberado, em vez do padrão do framework. |
| [`reduced-motion`](skills/design-ui/reduced-motion/SKILL.md) | Respeita prefers-reduced-motion sem quebrar o feedback da interface. |
| [`responsividade-mobile-first`](skills/design-ui/responsividade-mobile-first/SKILL.md) | Constrói layout partindo do mobile e ampliando por breakpoints. |
| [`ritmo-vertical`](skills/design-ui/ritmo-vertical/SKILL.md) | Ajusta leading, baseline e espaço entre blocos para ritmo constante. |
| [`semantica-e-aria`](skills/design-ui/semantica-e-aria/SKILL.md) | Usa HTML semântico primeiro e ARIA só quando necessário. |
| [`shadcn-ui`](skills/design-ui/shadcn-ui/SKILL.md) | Usa shadcn/ui como base de componentes e customiza via tokens, sem visual padrão. |
| [`tema-claro-escuro`](skills/design-ui/tema-claro-escuro/SKILL.md) | Implementa light e dark mode com tokens semânticos, incluindo opção "sistema". |
| [`tokens-de-cor`](skills/design-ui/tokens-de-cor/SKILL.md) | Define uma paleta fechada de 4-6 cores nomeadas como tokens semânticos. |
| [`transicoes-de-estado`](skills/design-ui/transicoes-de-estado/SKILL.md) | Anima a passagem entre estados preservando contexto. |
| [`voz-visual-da-marca`](skills/design-ui/voz-visual-da-marca/SKILL.md) | Define o mundo visual de uma marca — atitude, referências e o que ela nunca faz. |

### Ferramentas de dev & automação (15)

Como operar ferramentas de IA local e automação que uso: geração de imagem (ComfyUI, rembg), scraping/browser agent (browser-use, crawl4ai), RAG (AnythingLLM), voz (Pipecat), analytics self-hosted (Plausible), SEO (OpenSEO), gateway de LLM (OmniRoute), grafo de conhecimento de código (graphify), pentest automatizado (Strix), e otimização de consumo de tokens do próprio Claude Code (token-saver).

| Skill | Descrição |
|---|---|
| [`anything-llm`](skills/dev-tools/anything-llm/SKILL.md) | Opera o AnythingLLM local em Docker para RAG sobre documentos — workspaces, embeddings, agentes. |
| [`browser-use`](skills/dev-tools/browser-use/SKILL.md) | Automatiza o navegador com um agente LLM (Python + Playwright), sem seletores fixos. |
| [`cline`](skills/dev-tools/cline/SKILL.md) | Usa a extensão Cline no VS Code como agente de codificação com aprovação por passo e MCP. |
| [`comfyui`](skills/dev-tools/comfyui/SKILL.md) | Roda e monta workflows de geração de imagem em nós no ComfyUI local. |
| [`crawl4ai`](skills/dev-tools/crawl4ai/SKILL.md) | Extrai conteúdo de sites em markdown limpo para LLMs com Crawl4AI. |
| [`glm-5-2`](skills/dev-tools/glm-5-2/SKILL.md) | Referência de uso do modelo GLM-5.2 da Z.AI — endpoints, streaming, function calling. |
| [`graphify`](skills/dev-tools/graphify/SKILL.md) | Mapeia um projeto (código, docs, PDFs) em grafo de conhecimento consultável. |
| [`omniroute`](skills/dev-tools/omniroute/SKILL.md) | Usa o OmniRoute como gateway único de IA, compatível com OpenAI/Anthropic/Gemini. |
| [`open-seo`](skills/dev-tools/open-seo/SKILL.md) | Opera o OpenSEO — alternativa open-source a Semrush/Ahrefs. |
| [`pipecat`](skills/dev-tools/pipecat/SKILL.md) | Constrói agentes de voz e multimodais em tempo real com Pipecat. |
| [`plausible`](skills/dev-tools/plausible/SKILL.md) | Opera a instância local do Plausible Analytics (Community Edition em Docker). |
| [`public-apis`](skills/dev-tools/public-apis/SKILL.md) | Catálogo comunitário gigante de APIs públicas gratuitas por domínio. |
| [`rembg`](skills/dev-tools/rembg/SKILL.md) | Remove fundo de imagens localmente com rembg (ONNX/U2Net). |
| [`strix`](skills/dev-tools/strix/SKILL.md) | Roda o Strix, agente autônomo de pentest de código aberto. |
| [`token-saver`](skills/dev-tools/token-saver/SKILL.md) | Diagnostica, configura e otimiza o consumo de tokens do Claude Code. |

### Carreira (3)

Bots de automação de busca e candidatura a vagas.

| Skill | Descrição |
|---|---|
| [`careerbot`](skills/carreira/careerbot/SKILL.md) | Opera o CareerBot (Job-Hunter), bot Python/Selenium que candidata a vagas por critérios, com limite diário. |
| [`careerforge`](skills/carreira/careerforge/SKILL.md) | Roda o CareerForge dentro do Claude Code para achar vagas, escrever CV/carta sob medida e compilar em PDF. |
| [`linkedin-job-applier`](skills/carreira/linkedin-job-applier/SKILL.md) | Opera o LinkedIn AI Job Applier Ultimate, bot Python que auto-candidata no LinkedIn e Indeed. |

### Produtividade & escrita (2)

Como formatar resposta e revisar texto.

| Skill | Descrição |
|---|---|
| [`i-have-adhd`](skills/produtividade-escrita/i-have-adhd/SKILL.md) | Formata a resposta para leitor com TDAH: ação primeiro, passos numerados, estado reafirmado a cada turno. |
| [`no-ai-slop`](skills/produtividade-escrita/no-ai-slop/SKILL.md) | Edita rascunhos para uma escrita mais afiada e humana, preservando a voz do autor. |

## Como usar

### Claude Code / Claude Skills

Copie a pasta da skill que quiser para o diretório de skills do seu usuário ou projeto:

```bash
cp -r skills/design-ui/tokens-de-cor ~/.claude/skills/tokens-de-cor
```

O Claude carrega automaticamente o `SKILL.md` quando o pedido combina com a `description` do frontmatter.

### Como prompt de sistema em qualquer LLM

Cada `SKILL.md` também funciona como um bloco de instruções colável direto no system prompt de qualquer assistente (ChatGPT, Claude.ai, Gemini etc.) — não depende de nenhuma ferramenta específica. As skills de `dev-tools` referenciam ferramentas/CLIs específicas instaladas localmente; as de `design-ui`, `carreira` e `produtividade-escrita` são portáveis sem dependência de ambiente.

## Por que publicar isso

Escrever essas regras uma vez e reutilizar evita repetir o mesmo contexto (formato de data, como validar um merge, qual proporção de contraste usar, como estruturar um grid) em toda conversa nova. Publicar aqui serve tanto de backup versionado quanto de ponto de partida pra quem quiser adaptar pro próprio fluxo de trabalho.

Sinta-se à vontade para dar fork e ajustar ao seu domínio e ao seu estilo.

## Licença

[MIT](LICENSE) — use, adapte e distribua livremente.

---

## English

Personal library of Claude Skills I use for day-to-day work: data engineering, UI design, automation, local AI tooling, and job-search automation.

Inspired by repositories like [mentor-prompt](https://github.com/guithepc/mentor-prompt), this repo collects reusable pieces of my "second brain" — persistent instructions I load into Claude Code / Claude Skills so it already knows how I like code, design, and analysis delivered.

A **skill** here is a folder with a `SKILL.md` file (frontmatter `name` + `description`, instructions in the body) that Claude auto-loads when a request matches the description, plus optional reference files or scripts read on demand.

**68 skills across 5 groups:** `segundo-cerebro` (data engineering playbook), `design-ui` (46 single-principle design skills, combinable per project type), `dev-tools` (15 skills for local AI tooling and automation), `carreira` (3 job-search automation bots), `produtividade-escrita` (2 writing/output-format skills).

To use with Claude Code, copy the skill folder into `~/.claude/skills/`. Since each `SKILL.md` is plain Markdown, it also works as a system-prompt block for any LLM — the `dev-tools` skills reference locally installed tools/CLIs, while `design-ui`, `carreira` and `produtividade-escrita` are portable with no environment dependency.

MIT licensed — fork it and adapt it to your own domain and style.

