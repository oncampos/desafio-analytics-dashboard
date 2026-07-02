# Cartões · Painel Analítico — Desafio Analytics

Dashboard web interativo (single page) com a análise das transações de cartões de crédito e débito de uma cooperativa financeira — **Desafio 2** do processo seletivo de Analista de Dados.

**Período analisado:** 31/12/2018 a 20/02/2020 (fev/2020 é mês **parcial**, com dados até o dia 20).
**Fonte:** `db_cartoes.transacoes` + cadastros de associados e agências (dados fictícios do desafio).

## O que o painel entrega

- **KPI cards:** volume total (R$), transações, ticket médio, associados ativos e cartões ativos (pico mensal do intervalo — métrica não aditiva entre filtros, com tooltip explicativo).
- **Filtros interligados** (barra fixa no topo): cooperativa, agência (dependente da cooperativa), modalidade (toggle crédito/débito), faixa de renda e período (mês de/até). Todos os gráficos e KPIs recalculam a partir do cubo filtrado.
- **7 visões:** evolução mensal (barras empilhadas por modalidade + linha de transações), volume por cooperativa (com *cross-filter* por clique na barra), top 10 agências, volume por faixa de renda (rosca), top 10 cidades, mapa de calor dia da semana × hora e novos associados por mês (com anotação da queda de captação desde meados de 2019).
- **Transparência analítica:** fev/2020 sinalizado como parcial (`*` + nota de rodapé), notas de qualidade de dados (modalidade não informada em 2 transações; faixas 4 e 5 com a mesma descrição "ALTA"; encoding corrigido nos cadastros) e avisos sobre quais filtros se aplicam a cada corte agregado.

## Stack

| Camada | Tecnologia |
|---|---|
| Estrutura/estilo | HTML5 + CSS puro (grid responsivo, sem frameworks) |
| Lógica | JavaScript puro (vanilla) — estado dos filtros em objeto único, funções puras de agregação sobre o cubo |
| Gráficos | [Apache ECharts 5](https://echarts.apache.org/) via CDN (jsDelivr) — única dependência externa |
| Dados | `data.js` — cubo agregado (`const CUBE`) gerado na etapa de análise, ~250 KB |

Não há build, backend nem instalação de pacotes.

## Como rodar localmente

Basta abrir o `index.html` no navegador (duplo clique ou arrastar para o Chrome/Edge/Firefox). É necessário acesso à internet apenas para o CDN do ECharts.

```text
desafio-analytics-dashboard/
├── index.html   # dashboard completo (layout + lógica + gráficos)
├── data.js      # cubo de dados agregado (const CUBE)
├── .nojekyll    # desativa o Jekyll no GitHub Pages
└── README.md
```

## Como publicar no GitHub Pages

1. Crie um repositório no GitHub e envie os arquivos desta pasta:
   ```bash
   git init
   git add index.html data.js .nojekyll README.md
   git commit -m "Dashboard do desafio de analytics"
   git branch -M main
   git remote add origin https://github.com/<seu-usuario>/<seu-repo>.git
   git push -u origin main
   ```
2. No repositório, acesse **Settings → Pages**.
3. Em **Build and deployment**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)` e salve.
4. Em 1–2 minutos o painel estará disponível em `https://<seu-usuario>.github.io/<seu-repo>/`.

O arquivo `.nojekyll` (vazio) garante que o GitHub Pages sirva os arquivos estáticos diretamente, sem processamento Jekyll.

---

*Dados fictícios do desafio · fev/2020 parcial — leituras de tendência devem considerar essa limitação.*
