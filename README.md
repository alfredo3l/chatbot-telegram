🌤️ Bot Clima RocketSeat – Arquitetura Enterprise

n8n + Telegram + OpenAI + Gemini + OpenWeather

📌 Visão Geral

Este projeto implementa um Chatbot Inteligente de Clima no Telegram, desenvolvido em n8n, utilizando múltiplos modelos de IA e integração com a OpenWeather API para informar a temperatura atual de qualquer município do Brasil e do mundo.

A arquitetura foi projetada com separação clara de responsabilidades, controle de contexto por sessão, tratamento de erros e humanização dinâmica de respostas.

🧠 Arquitetura de Inteligência Artificial

O fluxo utiliza múltiplos modelos especializados:

🔹 OpenAI (gpt-4.1-mini)

Classificação de intenção

Humanização da resposta de temperatura

Agente de cumprimento

Extração estruturada da cidade

🔹 OpenAI Transcription

Transcrição de mensagens de áudio (OGG)

🔹 Google Gemini

Agente de fallback

Suporte adicional ao agente principal

🏗️ Arquitetura Técnica do Workflow
Telegram Trigger
      ↓
Switch (Texto ou Áudio)
      ↓
Transcrição (se áudio)
      ↓
Merge da entrada
      ↓
Classificador de Intenção (LLM)
      ↓
 ┌───────────────┬────────────────┬──────────────┐
Cumprimento   Previsão        Fallback
      ↓              ↓              ↓
Agente IA     Extrator Cidade   Agente Fallback
                    ↓
             Sanitização (IIFE)
                    ↓
           HTTP OpenWeather
                    ↓
                IF (200?)
               /        \
      Humanização     Tratamento Erro
           ↓
      Resposta Telegram

🧠 Controle de Memória Conversacional

O projeto utiliza:

Memory Buffer Window


Com:

sessionKey = chat.id do Telegram


Isso garante:

Contexto isolado por usuário

Evita repetição de saudação

Conversas independentes entre usuários

🎯 Funcionalidades Implementadas

✅ Classificação automática de intenção
✅ Extração estruturada da cidade
✅ Sanitização robusta de input
✅ Suporte a texto e áudio
✅ Humanização baseada na temperatura
✅ Controle de repetição de cumprimento
✅ Fallback especializado
✅ Tratamento de erro da API
✅ Controle de contexto por sessão
✅ Resposta personalizada com nome do usuário

🔎 Sanitização de Input (Proteção contra erro de API)

A cidade extraída passa por tratamento avançado:

Remove espaços extras

Converte para minúsculas

Remove acentos

Remove caracteres especiais

Normaliza múltiplos espaços

Implementado com IIFE no Set Node.

🌡️ Integração com OpenWeather

Endpoint utilizado:

https://api.openweathermap.org/data/2.5/weather


Query Parameters:

q → cidade sanitizada

units=metric

lang=pt_br

appid=sua_chave_aqui (placeholder)

⚠️ Atualmente a chave está como placeholder no node HTTP.

Recomendado para produção:

Variável de ambiente
OU

Credential nativa do n8n

🔐 Segurança – Permissões Mínimas Telegram

O bot necessita apenas:

✅ Receber mensagens privadas
✅ Enviar respostas

Não é necessário:

❌ Permissão administrativa em grupos
❌ Deletar mensagens
❌ Convidar usuários
❌ Fixar mensagens

Recomendado no BotFather:

/setprivacy → Enable


Isso impede que o bot monitore mensagens em grupo sem menção.

🧠 Classificação de Intenção

Categorias implementadas:

Cumprimento

Previsão do Tempo

FallBack

A classificação é feita por LLM com auto-fixing habilitado.

🌤️ Humanização Dinâmica da Temperatura

O agente principal adapta o tom conforme a faixa térmica:

Temperatura	Comportamento
> 30°C	Indica calor e sugere hidratação
20°C – 29°C	Clima agradável
15°C – 19°C	Clima ameno
< 15°C	Indica frio e sugere agasalho

⚠️ O foco principal é temperatura atual.

🎤 Suporte a Áudio

Fluxo:

Recebe áudio OGG

Baixa o arquivo via Telegram

Transcreve usando OpenAI

Processa como texto normal

⚠️ Tratamento de Erros

Caso a API retorne código diferente de 200:

Fluxo IF intercepta

Mensagem de erro é enviada ao usuário

⚠️ Em produção recomenda-se ocultar detalhes técnicos do erro.

⚙️ Variáveis Utilizadas (Placeholder)
OPENWEATHER_API_KEY=SUA_API_AQUI
TELEGRAM_BOT_TOKEN=SEU_TOKEN_AQUI


Atualmente o workflow mantém a chave como:

sua_chave_aqui


Recomendado substituir antes de deploy.

🚀 Deploy

Pode ser executado:

Localmente

Em VPS

Via Docker

Com domínio próprio e SSL

Requer:

Publicar workflow no n8n

Webhook ativo

Bot configurado

📈 Escopo do Projeto

✔ Temperatura atual
✔ Resposta humanizada
✔ Controle de contexto
✔ Multi-model LLM
✔ Tratamento robusto de input

Não implementado:

Histórico persistente de longo prazo

Cache de consultas

Dashboard administrativo

Monitoramento estruturado

🏆 Nível Arquitetural

Este projeto demonstra:

Orquestração de múltiplos LLMs

Separação clara de agentes

Sanitização segura de input

Uso correto de memória por sessão

Tratamento estruturado de erro

Design modular e escalável

👨‍💻 Projeto

Bot Clima RocketSeat
Arquitetura enterprise com n8n + IA + OpenWeather 🌤️
