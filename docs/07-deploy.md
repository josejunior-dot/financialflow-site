# 07 — Deploy

## Visao Geral

O **FinancialFlow Site** e hospedado no **GitHub Pages** como site estatico. Nao ha etapa de build — o deploy consiste em enviar os arquivos diretamente para o branch `master`, e o GitHub Pages serve os arquivos como estao.

**Configuracao atual:**

| Item | Valor |
|------|-------|
| Plataforma | GitHub Pages (legacy) |
| Repositorio | https://github.com/josejunior-dot/financialflow-site |
| Branch de deploy | `master` |
| Path | `/` (raiz do repositorio) |
| URL publica | https://josejunior-dot.github.io/financialflow-site/ |
| Build | Nenhum (HTML/CSS/JS puro) |

---

## Como fazer deploy

O deploy acontece automaticamente a cada `push` no branch `master`. O fluxo e:

```bash
# 1. Verificar as alteracoes
git status
git diff

# 2. Adicionar e commitar
git add -A
git commit -m "descricao das alteracoes"

# 3. Enviar para o GitHub (isso dispara o deploy)
git push origin master
```

Apos o push, o GitHub Pages reconstroi o site automaticamente. O processo leva de **1 a 2 minutos**.

---

## Verificar status do deploy

### Via GitHub CLI (`gh`)

```bash
# Listar os deployments recentes
gh api repos/josejunior-dot/financialflow-site/pages/builds --jq '.[0] | {status, created_at, error}'
```

### Via navegador

1. Acesse o repositorio no GitHub
2. Va em **Settings > Pages**
3. O status do ultimo deploy aparece no topo da pagina

### Via Actions (se houver workflow)

```bash
# Listar runs recentes do GitHub Actions
gh run list --repo josejunior-dot/financialflow-site --limit 5
```

---

## Forcar rebuild

Se o site nao atualizar apos o push, voce pode forcar um rebuild:

### Opcao 1 — Commit vazio

```bash
git commit --allow-empty -m "trigger rebuild"
git push origin master
```

### Opcao 2 — Via API do GitHub

```bash
gh api -X POST repos/josejunior-dot/financialflow-site/pages/builds
```

### Opcao 3 — Desabilitar e reabilitar o Pages

1. Va em **Settings > Pages**
2. Mude Source para **None** e salve
3. Mude de volta para **Deploy from a branch > master > / (root)** e salve

---

## Servir localmente para testes

Antes de fazer deploy, e recomendavel testar localmente.

### Com `npx serve`

```bash
# Na raiz do projeto
npx serve .
```

O servidor sobe em `http://localhost:3000` por padrao. Pressione `Ctrl+C` para encerrar.

### Com Python (alternativa)

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

Acesse `http://localhost:8000`.

### Com extensao Live Server (VS Code)

1. Instale a extensao **Live Server**
2. Clique com botao direito no `index.html`
3. Selecione **Open with Live Server**

---

## Compartilhar temporariamente com localtunnel

Para compartilhar o site local com outra pessoa (ex: para revisao), use o **localtunnel**:

```bash
# 1. Subir o servidor local
npx serve . -l 3000

# 2. Em outro terminal, criar o tunel
npx localtunnel --port 3000
```

O localtunnel gera uma URL publica temporaria (ex: `https://xyz-abc.loca.lt`) que qualquer pessoa pode acessar enquanto o tunel estiver ativo.

**Observacoes:**
- A URL e temporaria e muda a cada execucao
- O visitante pode precisar clicar em "Continue" na pagina de aviso do localtunnel
- Encerre ambos os processos (`serve` e `localtunnel`) com `Ctrl+C` quando terminar

---

## Possiveis problemas

### 404 no primeiro deploy

Apos habilitar o GitHub Pages pela primeira vez, o site pode retornar 404 por alguns minutos. Aguarde ate 10 minutos e tente novamente. Se persistir:

- Verifique se o branch `master` esta selecionado em **Settings > Pages**
- Confirme que existe um `index.html` na raiz do repositorio
- Force um rebuild (veja secao acima)

### Cache do navegador

Alteracoes no CSS ou JS podem nao aparecer imediatamente por causa do cache do navegador:

- **Hard refresh:** `Ctrl+Shift+R` (Windows/Linux) ou `Cmd+Shift+R` (Mac)
- **Limpar cache:** Abra DevTools (`F12`) > aba **Network** > marque **Disable cache** e recarregue
- **Query string:** Adicione `?v=2` ao final da URL para forcar o carregamento de uma versao nova

### Arquivo CSS/JS nao carrega (MIME type)

Se o GitHub Pages nao reconhecer o tipo do arquivo, verifique:

- Extensoes corretas (`.css`, `.js`)
- Caminhos relativos corretos (sem `/` no inicio, pois o site roda em subpath `/financialflow-site/`)

### Site desatualizado apos push

Se o push foi feito mas o site nao atualiza:

1. Verifique o status do build (secao acima)
2. Aguarde 2-3 minutos
3. Force um rebuild se necessario
4. Limpe o cache do navegador

---

## Configurar dominio customizado (futuro)

Para usar um dominio proprio (ex: `www.financialflow.com.br`) no lugar da URL do GitHub Pages:

### 1. Registrar o dominio

Registre o dominio em um provedor (ex: Registro.br, Cloudflare, Namecheap).

### 2. Configurar DNS

Adicione os seguintes registros DNS no seu provedor:

**Para dominio apex (financialflow.com.br):**

| Tipo | Nome | Valor |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**Para subdominio (www.financialflow.com.br):**

| Tipo | Nome | Valor |
|------|------|-------|
| CNAME | www | josejunior-dot.github.io |

### 3. Configurar no GitHub

```bash
# Via CLI
gh api -X PUT repos/josejunior-dot/financialflow-site/pages \
  --field cname="www.financialflow.com.br"
```

Ou manualmente:

1. Va em **Settings > Pages**
2. Em **Custom domain**, digite o dominio
3. Marque **Enforce HTTPS** (apos a verificacao DNS)

### 4. Criar arquivo CNAME

Crie um arquivo `CNAME` na raiz do repositorio com o dominio:

```
www.financialflow.com.br
```

```bash
echo "www.financialflow.com.br" > CNAME
git add CNAME
git commit -m "add custom domain"
git push origin master
```

### 5. Aguardar propagacao

A propagacao DNS pode levar ate 24-48 horas. O certificado HTTPS (Let's Encrypt) e emitido automaticamente pelo GitHub apos a verificacao do dominio.

---

## Resumo rapido

```bash
# Deploy
git add -A && git commit -m "mensagem" && git push origin master

# Verificar status
gh api repos/josejunior-dot/financialflow-site/pages/builds --jq '.[0].status'

# Forcar rebuild
git commit --allow-empty -m "trigger rebuild" && git push origin master

# Testar local
npx serve .

# Compartilhar temporariamente
npx serve . -l 3000 & npx localtunnel --port 3000
```
