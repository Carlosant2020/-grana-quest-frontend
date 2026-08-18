# GranaQuest — Frontend (conectado à API real)

Esta é a versão do app que fala de verdade com o backend (login, gastos, orçamentos, gamificação e chat persistidos no seu Postgres).

## Por que não posso simplesmente dar dois cliques no index.html?

Diferente do protótipo anterior (que funcionava sozinho), esse frontend faz chamadas para `http://localhost:4000`. Navegadores bloqueiam esse tipo de chamada (CORS) quando a página é aberta direto do disco (`file://...`), porque a origem não bate com a que o backend espera (`http://localhost:5173`, configurada no `.env` do backend).

A solução é servir esse `index.html` por um servidor local simples, na porta 5173.

## Como rodar

Com o **backend já rodando** (`npm run dev` na pasta `grana-quest-backend`), abra um terminal **nesta pasta** (`grana-quest-frontend`) e escolha uma opção:

### Opção A — com Node (recomendado, já que você tem Node instalado)
```bash
npx serve -l 5173
```
Na primeira vez ele vai perguntar se pode instalar o pacote `serve` — digite `y`. Depois acesse:
```
http://localhost:5173
```

### Opção B — com Python (se tiver Python instalado)
```bash
python -m http.server 5173
```
Depois acesse:
```
http://localhost:5173
```

## Login

Use a mesma conta que você já criou testando a API (ex: `carlosantoniodelfino@gmail.com`), ou crie uma nova pela própria tela de "Criar conta" do app agora.

## Se aparecer o aviso vermelho de "não foi possível falar com o backend"

Checklist:
1. O backend está rodando? (`npm run dev` na outra pasta, sem erros)
2. Você está acessando via `http://localhost:5173` (servido) e não abrindo o arquivo direto (`file://...`)?
3. O `.env` do backend tem `FRONTEND_URL="http://localhost:5173"`? Se você serviu em outra porta, ajuste esse valor no `.env` do backend e reinicie o `npm run dev`.

## Ajustando a porta da API

Se seu backend estiver rodando em outra porta, edite a constante no topo do `index.html`:

```js
const API_BASE = 'http://localhost:4000/api/v1';
```

## Nota sobre persistência da sessão

O token de acesso fica só na memória da página (não usamos localStorage). Isso significa que, ao recarregar a aba, você precisa entrar de novo — é uma escolha de segurança simples para este estágio do projeto. Uma versão mais completa usaria o refresh token (que já existe no backend, via cookie) de forma mais transparente no carregamento inicial da página.
