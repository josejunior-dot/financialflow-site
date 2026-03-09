# 01 — Instalacao e Setup

## Visao Geral

O **FinancialFlow Site** e uma landing page estatica para o produto LeadFlow Financial (CRM com IA e Multicalculo para assessores de investimento). Nao utiliza frameworks, bundlers ou ferramentas de build — e composto por um unico arquivo HTML com CSS inline e JavaScript vanilla.

**Stack:**
- HTML5
- CSS inline (variaveis CSS customizadas)
- JavaScript vanilla (animacoes, interacoes)
- Lucide Icons (via CDN)
- Google Fonts (Inter)

---

## Pre-requisitos

### Minimo (apenas visualizar)
- Um navegador web moderno (Chrome, Firefox, Edge, Safari)
- Nenhuma instalacao adicional e necessaria

### Para servir localmente com live reload
- **Node.js** (v18+) — apenas para usar `npx serve`
- **Git** — para clonar o repositorio

### Para deploy
- Conta no **GitHub** com acesso ao repositorio
- GitHub Pages habilitado no branch `master`

---

## Setup Local

### 1. Clonar o repositorio

```bash
git clone https://github.com/josejunior-dot/financialflow-site.git
cd financialflow-site
```

### 2. Abrir no navegador (forma mais simples)

Basta abrir o arquivo `index.html` diretamente no navegador:

- **Windows:** duplo clique no `index.html` ou arraste para o navegador
- **Linux/Mac:** `open index.html` (Mac) ou `xdg-open index.html` (Linux)

> **Nota:** Algumas funcionalidades que dependem de requisicoes HTTP (como carregamento de icones Lucide via CDN) precisam de conexao com a internet. Fora isso, tudo funciona offline.

### 3. Servir com servidor local (recomendado para desenvolvimento)

Usar um servidor HTTP local evita problemas de CORS e simula melhor o ambiente de producao:

```bash
npx serve .
```

O servidor inicia por padrao em `http://localhost:3000`. Para usar outra porta:

```bash
npx serve . -l 8080
```

Alternativas sem Node.js:

```bash
# Python 3
python -m http.server 3000

# PHP
php -S localhost:3000
```

---

## Estrutura do Projeto

```
financialflow-site/
├── index.html          # Pagina principal (HTML + CSS + JS, ~900 linhas)
├── logo.png            # Logo do produto
├── docs/               # Documentacao do projeto
│   └── 01-installation.md
└── index.html.bak      # Backup do HTML
```

- **Nao ha** `package.json`, `node_modules`, ou qualquer dependencia local
- **Nao ha** etapa de build — o HTML e servido diretamente
- Icones sao carregados via CDN do Lucide (`unpkg.com`)
- Fonte Inter e carregada via Google Fonts CDN

---

## Deploy (GitHub Pages)

O deploy e automatico via GitHub Pages. O fluxo e:

### 1. Fazer alteracoes e commit

```bash
git add index.html
git commit -m "Descricao da alteracao"
```

### 2. Push para o branch master

```bash
git push origin master
```

### 3. GitHub Pages publica automaticamente

O site fica disponivel em:

```
https://josejunior-dot.github.io/financialflow-site/
```

### Configuracao do GitHub Pages (caso necessario)

Se o GitHub Pages nao estiver configurado:

1. Acesse o repositorio no GitHub
2. Va em **Settings** > **Pages**
3. Em **Source**, selecione o branch `master`
4. Em **Folder**, selecione `/ (root)`
5. Clique em **Save**
6. Aguarde alguns minutos para o primeiro deploy

---

## Troubleshooting

### Icones nao aparecem

**Causa:** Os icones Lucide sao carregados via CDN. Se nao aparecerem:

- Verifique sua conexao com a internet
- Verifique no DevTools (F12 > Console) se ha erros de carregamento do script Lucide
- O CDN usado e `unpkg.com/lucide@latest` — se estiver fora do ar, aguarde ou troque para outro CDN

### Fonte Inter nao carrega

**Causa:** A fonte e carregada via Google Fonts CDN.

- Verifique a conexao com a internet
- O site usa a fonte Inter com pesos 300-900; se o Google Fonts estiver indisponivel, o fallback e `-apple-system, BlinkMacSystemFont, sans-serif`

### Pagina em branco ao abrir o index.html

- Verifique se o arquivo `index.html` nao esta corrompido
- Tente abrir em outro navegador
- Verifique o console do navegador (F12) para erros de JavaScript

### GitHub Pages nao atualiza apos push

- O deploy pode levar de 1 a 5 minutos
- Verifique em **Settings > Pages** se o deploy esta ativo
- Acesse **Actions** no repositorio para ver se ha erros no workflow de deploy
- Limpe o cache do navegador (`Ctrl+Shift+R`) para forcar o recarregamento

### Estilos quebrados / layout desalinhado

- O CSS usa variaveis CSS (`--primary`, `--radius`, etc.) definidas em `:root` — verifique se a secao `<style>` esta intacta
- O site e responsivo; teste em diferentes tamanhos de tela usando DevTools (F12 > Toggle Device Toolbar)

### CORS ao abrir index.html direto (file://)

Alguns navegadores bloqueiam requisicoes de CDN quando o arquivo e aberto via protocolo `file://`. Solucao:

```bash
npx serve .
```

Isso serve o arquivo via `http://localhost:3000`, evitando restricoes de CORS.

---

## Links Uteis

- **Repositorio:** https://github.com/josejunior-dot/financialflow-site
- **Site em producao:** https://josejunior-dot.github.io/financialflow-site/
- **Lucide Icons:** https://lucide.dev/
- **Google Fonts (Inter):** https://fonts.google.com/specimen/Inter
