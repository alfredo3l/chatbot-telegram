# 📘 README

Este projeto implementa um **Chatbot Inteligente de Clima no Telegram**, desenvolvido no **n8n**, que consulta a **OpenWeather API** para retornar a **temperatura atual de qualquer município do Brasil e do mundo** informado pelo usuário.

O bot possui:

- Tratamento inteligente de mensagens
- Identificação de cumprimento
- Respostas dinâmicas e humanizadas
- Agente de fallback para mensagens fora do contexto
- Integração com memória de conversa
- Experiência amigável e profissional

---

# 🌤️ Visão Geral do Projeto

O sistema é composto por múltiplos agentes organizados no workflow:

1. **Classificador de intenção**
2. **Agente principal de temperatura**
3. **Agente fallback (fora de contexto)**
4. **Integração com OpenWeather**
5. **Resposta dinâmica personalizada**

O objetivo é oferecer uma experiência natural, amigável e focada exclusivamente em **temperatura atual**.

---

# 📌 Funcionalidades

- ✅ Integração com **Telegram Bot**
- ✅ Consulta de temperatura em tempo real via **OpenWeather**
- ✅ Identificação automática de cumprimento
- ✅ Resposta personalizada com nome do usuário
- ✅ Resposta adaptativa conforme temperatura (frio, ameno, quente)
- ✅ Tratamento de mensagens fora de contexto
- ✅ Experiência humanizada
- ✅ Suporte a mensagens de texto e áudio
- ✅ Workflow contínuo (publicado)

---

# 🧠 Inteligência Conversacional

O bot possui três comportamentos principais:

## 1️⃣ Cumprimento Inicial

Quando o usuário envia:

- Olá
- Oi
- Bom dia
- Boa tarde
- Boa noite

O bot:

- Cumprimenta pelo nome
- Informa data e hora atual
- Explica que é especializado em temperatura
- Informa que aceita texto e áudio

Evita repetição caso já tenha cumprimentado anteriormente (controle de memória).

---

## 2️⃣ Consulta de Temperatura

Quando o usuário pergunta:

- Qual a temperatura em Brasília?
- Temperatura em São Paulo
- Como está o clima em Lisboa?

O fluxo:

1. Identifica a cidade
2. Consulta OpenWeather
3. Retorna a temperatura atual
4. Humaniza a resposta conforme o valor:

| Faixa de Temperatura | Comportamento |
|----------------------|--------------|
| Acima de 30°C        | Indica calor |
| 20°C – 29°C          | Clima agradável |
| 15°C – 19°C          | Clima ameno |
| Abaixo de 15°C       | Indica frio |

⚠️ O bot **não fornece previsão futura**, apenas temperatura atual.

---

## 3️⃣ Mensagens Fora de Contexto (Fallback)

Se o usuário enviar algo como:

- “Me dê uma receita de bolo”
- “Conte uma piada”
- “Quem descobriu o Brasil?”

O agente fallback responde cordialmente:

> Este assistente é especializado em informar a temperatura atual de municípios do Brasil e do mundo 🌤️  
> Esse tipo de solicitação não faz parte do seu campo de atuação.

E orienta o usuário a reformular dentro do contexto correto.

---

# 📂 Estrutura do Workflow

Fluxo principal:

1. **Telegram Trigger**  
   Recebe mensagens do usuário.

2. **Classificador de Intenção**  
   Identifica:
   - Cumprimento
   - Consulta de temperatura
   - Fora de contexto

3. **Tratamento de Cumprimento**  
   Gera resposta inicial personalizada.

4. **Preparar Query OpenWeather**  
   Monta a requisição HTTP.

5. **Consultar OpenWeather (HTTP Request)**  
   Chamada à API.

6. **Formatação Dinâmica da Resposta**  
   Transforma:

   🌤️ A temperatura em Cidade é de XX°C

   em resposta humanizada.

7. **Fallback (fora de contexto)**  
Resposta redirecionadora.

8. **Telegram – Enviar Mensagem**  
Retorna resposta ao usuário.

---

# 🚀 Como importar o workflow no n8n

1. Acesse o painel do n8n.
2. Vá em **Workflows → Import from file**.
3. Selecione o arquivo JSON.
4. Salve o workflow.

---

# 🔐 Configuração das Credenciais

## 1️⃣ Telegram Bot

### Criar o Bot

1. No Telegram, converse com **@BotFather**.
2. Use `/newbot`.
3. Copie o **Bot Token**.

### Configurar no n8n

1. Vá em **Credentials → New**
2. Escolha **Telegram API**
3. Insira o Bot Token
4. Salve

---

## 2️⃣ OpenWeather API

### Obter API Key

1. Acesse:
https://openweathermap.org/
2. Crie uma conta
3. Gere uma API Key

---

### Configurar no n8n

#### Opção A — Variável de Ambiente (Recomendado)

Defina:

OPENWEATHER_API_KEY=sua_chave_aqui


Reinicie o n8n após definir.

#### Opção B — Credencial no n8n

1. Vá em **Credentials → New**
2. Escolha **HTTP Header Auth** ou similar
3. Insira a API Key
4. Associe ao nó HTTP

---

# ⚙️ Variáveis Utilizadas

| Variável | Descrição |
|----------|----------|
| OPENWEATHER_API_KEY | Chave da API OpenWeather |
| TELEGRAM_BOT_TOKEN | Token do Bot Telegram |

---

# ▶️ Publicar o Workflow (Obrigatório)

1. Abra o workflow
2. Clique em **Publish**
3. Após publicar:
   - O webhook é registrado
   - O bot passa a responder automaticamente

⚠️ Se reiniciar máquina ou usar ngrok, será necessário publicar novamente.

---

# 🧪 Como Usar o Chatbot

No Telegram, envie:

### Exemplos válidos:

- Qual a temperatura em Brasília?
- Temperatura em São Paulo
- Como está o clima em Lisboa?
- Rio de Janeiro

---

## ✅ Exemplo de Resposta

Alfredo, neste momento a temperatura em Brasília está em 32°C ☀️  

Está um clima bem quente por aí.

---

## ❌ Exemplo Fora de Contexto

Pergunta:
> Me dê uma receita de bolo

Resposta:
> Este assistente é especializado em informar a temperatura atual de municípios do Brasil e do mundo 🌤️  
> Esse tipo de solicitação não faz parte do seu campo de atuação.

---

# 🏗️ Tecnologias Utilizadas

- **n8n**
- **Telegram Bot API**
- **OpenWeather API**
- **HTTP Request Node**
- **IF Nodes (validação lógica)**

---

# 🎯 Escopo do Projeto

✔️ Temperatura atual  
✔️ Resposta humanizada  
✔️ Tratamento de erro  
✔️ Controle de contexto  

❌ Não fornece previsão futura  
❌ Não responde perguntas gerais  
❌ Não executa múltiplas funções  

---

# 📈 Evoluções Futuras Possíveis

- Sensação térmica
- Umidade
- Condição climática (chuva, nublado)
- Histórico de consultas
- Dashboard administrativo

---

# 👨‍💻 Autor

Projeto desenvolvido com n8n + OpenWeather + Telegram  
Chatbot especializado em temperatura atual 🌤️

