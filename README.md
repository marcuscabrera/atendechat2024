# Atendechat 6.0.0

## Visão Geral
Atendechat é uma plataforma omnichannel de atendimento com backend em Node.js/TypeScript e frontend em React. O repositório é organizado como um monorepo com as pastas `backend/`, `frontend/` e `install/`, cobrindo desde APIs e filas de processamento até a interface web administrativa e scripts de implantação.

## Backend (Node.js/TypeScript)
O backend fica em `backend/` e expõe uma API REST com Socket.IO para comunicação em tempo real. Principais características:

- **Inicialização e servidor**: carrega variáveis de ambiente, configura Express com CORS, cookies, Sentry e expõe um diretório público para uploads. O servidor inicia filas de mensagens, jobs recorrentes e sessões do WhatsApp.
- **Autenticação e rotas**: utiliza JWT, cookies seguros e middlewares de autorização. As rotas cobrem módulos como usuários, contatos, tickets, campanhas, prompts, integrações, gerenciamento de filas e outros recursos.
- **Banco de dados**: usa Sequelize (MySQL por padrão, com suporte a outros dialetos via variáveis de ambiente) com charset UTF8MB4. Há dezenas de modelos para tickets, campanhas, chats, arquivos, filas e multiempresa.
- **Filas e agendamentos**: integra Bull/Redis para envio de mensagens, campanhas, agendamentos e monitoramentos. Os jobs utilizam nodemailer, Mustache, data-fns e notificações em tempo real.
- **Websocket**: Socket.IO valida o JWT, gerencia presença e salas por empresa/usuário/status, garantindo ressincronização de inscrições e atualizações instantâneas.
- **Integração WhatsApp**: serviços Wbot baseados em Baileys criam sessões e enviam mensagens (texto e mídia), gerando automaticamente URLs públicas para arquivos armazenados.

## Frontend (React)
O frontend em `frontend/` entrega um painel administrativo completo. Destaques:

- **Stack**: React 17 com React Query, Material-UI (v4/v5), theming claro/escuro e i18n padrão PT-BR.
- **Autenticação**: contexto próprio faz interceptação de requisições Axios, refresh de tokens, controle de login/logout e integra com o gerenciador de sockets.
- **Comunicação em tempo real**: provedor global de Socket.IO sincroniza tickets, filas e presença em múltiplos canais.
- **Recursos da interface**: dashboards (Chart.js, Recharts), Kanban, gerenciamento de conexões WhatsApp, campanhas, arquivos, prompts, gravação de áudio e notificações.
- **Cliente HTTP**: instâncias Axios configuradas via `REACT_APP_BACKEND_URL`, separando requisições com e sem credenciais.

## Scripts de Instalação (`install/`)
A pasta `install/` contém scripts shell para instalação primária e secundária do ambiente Atendechat. O fluxo recomendado é:

```bash
sudo apt update
sudo apt install -y git
cd /opt # ou outro diretório de sua preferência
sudo git clone https://github.com/marcuscabrera/atendechatinstall
sudo chmod -R 777 atendechatinstall
cd atendechatinstall
sudo ./install_primaria
```

Os scripts configuram dependências como Node.js, banco de dados, Redis e serviços necessários para executar backend e frontend. Consulte os arquivos dentro de `install/` para customizar parâmetros ou executar a instalação secundária.

## Próximos Passos
- Configure as variáveis de ambiente exigidas pelo backend (`.env`) e frontend (`.env`).
- Execute migrations/seeds conforme a documentação interna do backend.
- Inicie backend e frontend para utilizar o painel administrativo.

## Licença
Todos os direitos reservados a [https://atendechat.com](https://atendechat.com).
