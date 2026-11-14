# Atividade 5 — Requisição HTTP (Consulta de CEPs)

Aplicação web que consulta endereços a partir de um CEP usando a API pública [ViaCEP](https://viacep.com.br/). O front-end faz uma requisição HTTP com `fetch` e o back-end em Express serve os arquivos estáticos.

Atividade da disciplina de Desenvolvimento Web — DSM / Fatec.

## Tecnologias

- **Node.js** + **Express** (servidor de arquivos estáticos)
- **dotenv** (configuração da porta via `.env`)
- **HTML**, **CSS** e **JavaScript** puro no front-end
- **Docker** / **Docker Compose**

## Estrutura

```
.
├── server/
│   └── main.js              # Servidor Express
├── public/
│   ├── index.html           # Página principal
│   └── assets/
│       ├── css/index.css
│       ├── js/script.js     # Lógica da consulta ao ViaCEP
│       └── images/          # Logos DSM, Fatec e CPS
├── Dockerfile
├── compose.yaml
├── .env                     # PORT=3001
└── package.json
```

## Como funciona

1. O usuário digita um CEP (8 dígitos, com ou sem hífen — ex.: `12328-070`) e pressiona **Enter**.
2. O script valida o formato com uma expressão regular.
3. É feita uma requisição `GET` para `https://viacep.com.br/ws/{cep}/json`.
4. A resposta é tratada:
   - erro na requisição → "Erro ao consultar o serviço. Tente novamente."
   - `{ "erro": true }` → "CEP não encontrado."
   - sucesso → os dados são exibidos na página.

## Executando localmente

Pré-requisito: Node.js 20.11+ (o servidor usa `import.meta.dirname`).

```bash
npm install
npm start        # ou: npm run dev (reinicia ao salvar)
```

Acesse `http://localhost:3001` (porta definida no `.env`; sem ele, a padrão é `3000`).

## Executando com Docker

```bash
docker compose up --build
```

Acesse `http://localhost:3002`.

## Scripts

| Comando       | Descrição                                   |
|---------------|---------------------------------------------|
| `npm start`   | Inicia o servidor                           |
| `npm run dev` | Inicia com `node --watch` (recarga automática) |
