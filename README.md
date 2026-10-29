# ⚽ Arquibancada IA — Chatbot das Copas do Mundo

Projeto acadêmico: frontend HTML/CSS/JS e backend Flask + Groq. Responde somente sobre Copas do Mundo de futebol da FIFA.

## Estrutura
- `backend/app.py`: API, validação de escopo, prompt de sistema e integração Groq.
- `frontend/`: interface estática e configuração da URL da API.
- `tests/`: testes automatizados básicos.
- `render.yaml`: deploy do backend no Render.

## Executar localmente
1. Instale Python 3.11+ e `uv`.
2. `cp .env.example .env` (no PowerShell: `Copy-Item .env.example .env`).
3. Preencha `GROQ_API_KEY` em `.env` com uma chave válida obtida no console Groq.
4. `uv sync`
5. `uv run python backend/app.py`
6. Em outro terminal, `cd frontend` e `python -m http.server 5500`.
7. Abra `http://localhost:5500`.

Execute testes: `uv run pytest -q`.

## Publicar no Render
1. Envie o repositório para o GitHub Classroom.
2. No Render, crie um serviço Web a partir do repositório, ou use o Blueprint `render.yaml`.
3. Configure `GROQ_API_KEY` e `FRONTEND_ORIGINS` nas variáveis de ambiente do Render (nunca no GitHub).
4. A origem CORS deve ser exata, por exemplo `https://usuario.github.io` para GitHub Pages ou `https://nome.netlify.app` para Netlify. Sem barras finais e sem caminho.
5. Confirme `https://SEU_BACKEND.onrender.com/api/health`.

## Publicar o frontend
**Netlify:** publique a pasta `frontend` como diretório estático. Antes do deploy, altere `frontend/config.js` para `window.API_BASE_URL = 'https://SEU_BACKEND.onrender.com';`.

**GitHub Pages:** em Settings > Pages, selecione GitHub Actions e utilize o workflow incluso. O site ficará em `https://USUARIO.github.io/NOME-REPO/`. Altere `frontend/config.js` com a URL pública do Render e envie um novo commit.

Após o deploy, revise `FRONTEND_ORIGINS` no Render e faça um teste de ponta a ponta pelo navegador.

## API
`POST /api/chat` com JSON `{"message":"Quem venceu a Copa do Mundo de 2002?"}` retorna `{"reply":"...", "refused":false}`. `GET /api/health` retorna status.

## Limitações e segurança
A verificação de escopo usa regras conservadoras de palavras-chave e o prompt da IA como segunda camada. **Não é uma garantia absoluta**: perguntas mistas e tentativas de prompt injection que contenham termos de Copa podem passar pela checagem lexical. Para uso com requisitos rigorosos, adicione um classificador independente com política fail-closed, filtre perguntas mistas e valide também a resposta gerada. Não armazene a chave no frontend. Não envie dados pessoais à API. Para produção, adicione rate limiting, monitoramento e testes adversariais. O Render gratuito pode hibernar após inatividade.

## Alterei aqui
Nesse ponto eu alterei de forma remota.
## Alterei aqui local
Aqui estou fazendo uma alteração local.