# Agno WAHA WhatsApp Bot

## Descrição

O **Agno WAHA WhatsApp Bot** é uma solução de automação de atendimento via WhatsApp, integrando inteligência artificial (IA) baseada em LLM e APIs de automação, viabilizando **respostas automáticas inteligentes** e integração fácil com fluxos comerciais e de suporte. Projetado para atender empresas como a "Personalizando Sonhos – Loja de Informática \& Artesanato", o bot pode ser adaptado para outros segmentos.[^1]

- **Backend** construído com **FastAPI** e **Celery**
- Integração com **WAHA API** para automação do WhatsApp
- Suporte a **prompt personalizado e cache semântico**
- Pronto para deploy local ou containerizado via **Docker Compose**

***

## Exibição de Teste do Bot no Painel do WAHA

<a href="https://claudiomendonca.eng.br"><img align="right" alt="Developer vector created by storyset - www.freepik.com" height="330" src="https://github.com/ProfMPPDias/Agno_Waha_Whatsapp_Bot/blob/main/test/Whatsapp_Agno.png"></a>

***
## Estrutura do Projeto

```
Agno_Waha_Whatsapp_Bot/
│
├── app.py              # Inicialização do FastAPI
├── compose.yml         # Configuração Docker/WAHA
├── pyproject.toml      # Configuração de dependências Python
├── uv.lock             # Lockfile das dependências Python
├── .env                # Variáveis de ambiente sensíveis (NÃO subir para GitHub)
├── .gitignore          # Exclusões do Git
├── LICENSE             # Licença GPLv3 do projeto
├── README.md           # Documentação do projeto
│
├── routers/            # Rotas FastAPI (ex: waha_router.py)
├── services/           # Serviços (ex: waha_service.py)
├── workers/            # Workers Celery (ex: tasks.py)
├── scripts/            # Scripts auxiliares
├── data/               # Dados e assets da aplicação
├── .devcontainer/      # Ambientes DevContainer (VS Code)
 └── ...
```


***

## Tecnologias Utilizadas

- **FastAPI** — Backend e APIs HTTP
- **Celery** — Workers de tarefas assíncronas e orquestração
- **WAHA API** — Integração com WhatsApp ([devlikeapro/waha:latest])
- **Docker Compose** — Orquestração de containers para deploy rápido
- **Agno (IA)** — Motor de LLM e cache semântico
- **Python ≥ 3.13**

***

## Requisitos

- Python **3.13** ou superior
- Docker e Docker Compose (opcional, mas recomendado)
- Conta e credenciais para WAHA API (devlikeapro)
- API Key OpenAI, Gemini ou outra IA suportada (para LLM/Agno)
- RabbitMQ em execução (para Celery)

***

## Instalação Manual (Ambiente Local)

### 1. Clone o repositório

```bash
git clone https://github.com/suarepo/Agno_Waha_Whatsapp_Bot.git
cd Agno_Waha_Whatsapp_Bot
```


### 2. Crie e ative o ambiente virtual

```bash
python3 -m venv .venv
source .venv/bin/activate
```


### 3. Instale as dependências

```bash
pip install -r requirements.txt  # ou: pip install . se usar pyproject.toml/poetry
```


### 4. Configure o arquivo `.env`

Crie um arquivo `.env` na raiz com suas chaves/credentials:

```
OPENAI_API_KEY=suachave...
WAHA_API_URL=https://url-da-waha
WAHA_SESSION_NAME=nomedasesao
RABBITMQ_URL=pyamqp://guest:guest@localhost//
```

*Atenção: Nunca suba seu `.env` para o GitHub.*

***

### 5. Execute os serviços

#### FastAPI (API)

```bash
uvicorn app:app --reload
```


#### Celery (Worker)

```bash
celery -A workers.tasks worker --loglevel=info
```


#### (Opcional) Suba tudo via Docker Compose

```
docker-compose up --build
```

Verifique as configurações e variáveis no `compose.yml`.

***

## Exemplo de Uso

- Gere um QR code de sessão WhatsApp via WAHA
- Inicie o bot
- Envie mensagens para seu número WhatsApp cadastrado — o bot responderá automaticamente segundo o prompt e scripts configurados

***

## Estrutura das Rotas

- **POST /waha/webhook**: Recebe mensagens do WhatsApp e processa via IA e regras
- Serviços e integrações podem ser estendidos via scripts em `/services` e `/workers`

***

## Personalização

Edite o arquivo `prompt.xml` para customizar o comportamento do atendente virtual. Os dados institucionais estão em `personalizando.md`. Para adaptar para outras empresas, edite/escreva as informações de contato, horários e áreas de atuação.

***

## Licença

Distribuído sob a **GNU GPLv3**. Consulte o arquivo LICENSE para detalhes.

