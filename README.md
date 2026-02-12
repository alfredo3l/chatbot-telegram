

# 📘 README

Este projeto implementa um **chatbot de clima no Telegram**, desenvolvido no **n8n**, que consulta a **OpenWeather API** para retornar a temperatura atual de uma cidade brasileira informada pelo usuário.

O bot valida o formato da entrada, consulta a API de clima e responde automaticamente no Telegram sempre que o usuário enviar uma nova mensagem.

---

# 📌 Funcionalidades

- Integração com **Telegram Bot**
- Consulta de clima em tempo real via **OpenWeather**
- Validação de entrada no formato `Cidade,UF`
- Respostas automáticas e contínuas (workflow publicado)
- Tratamento de erro para cidades inválidas

---

# 📂 Estrutura do Workflow

Fluxo principal do workflow:

1. **Telegram Trigger**  
   Recebe mensagens enviadas ao bot.

2. **Entrada (cidade/UF)**  
   Normaliza e prepara a entrada do usuário.

3. **Formato válido? (IF)**  
   Verifica se a entrada segue o padrão `Cidade,UF`.

4. **Montar query (q)**  
   Constrói a query no formato aceito pela OpenWeather (`Cidade,UF,BR`).

5. **Consultar OpenWeather**  
   Realiza a chamada HTTP para a OpenWeather API.

6. **Status 200? (IF)**  
   Verifica se a resposta da API indica sucesso.

7. **Mensagem: sucesso / Mensagem: erro**  
   Monta a resposta adequada para o usuário.

8. **Telegram – Enviar mensagem**  
   Envia a resposta final ao chat do usuário.

---

# 🚀 Como importar o workflow no n8n

1. Acesse o painel do n8n.
2. Vá em **Workflows → Import from file**.
3. Selecione o arquivo JSON do workflow.
4. Salve o workflow.

---

# 🔐 Configuração das credenciais

## 1️⃣ Telegram Bot

### Criar o bot

1. No Telegram, converse com o **@BotFather**.
2. Crie um novo bot usando `/newbot`.
3. Copie o **Bot Token** fornecido.

### Configurar no n8n

1. Vá em **Credentials → New**.
2. Escolha **Telegram API**.
3. Preencha:
   - **Bot Token:** `TELEGRAM_BOT_TOKEN`
4. Salve a credencial.

---

## 2️⃣ OpenWeather API

### Obter a API Key

1. Crie uma conta em:  
   https://openweathermap.org/
2. Gere uma **API Key** no painel da conta.

---

### Configurar no n8n

### Opção A — Variável de ambiente (recomendado)

Defina no ambiente onde o n8n está rodando (ex: Docker):


Reinicie o n8n após adicionar a variável.

---

### Opção B — Credencial do n8n

1. Vá em **Credentials → New**.
2. Escolha **OpenWeatherMap API**.
3. Insira a API Key.
4. Associe a credencial ao nó **Consultar OpenWeather**.

---

# ⚙️ Variáveis esperadas

| Variável              | Descrição                         |
|-----------------------|----------------------------------|
| OPENWEATHER_API_KEY   | Chave da OpenWeather API         |
| TELEGRAM_BOT_TOKEN    | Token do bot do Telegram         |

---

# ▶️ Publicar o workflow (obrigatório)

Para que o bot funcione continuamente:

1. Abra o workflow no n8n.
2. Clique em **Publish / Publicar** no topo da tela.
3. Após publicado:
   - O webhook é registrado no Telegram
   - O bot passa a responder sempre que receber mensagens

⚠️ Se você reiniciar a máquina ou usar ngrok, será necessário publicar novamente.

---

# 🧪 Como usar o chatbot

No Telegram, envie mensagens no formato:


### Exemplos:

Cidade,UF

---

## ✅ Resposta de sucesso

☁️ A temperatura em Curitiba é de 24°C

---

## ❌ Resposta de erro


❌ Cidade não encontrada. Use o formato Cidade,UF (ex.: São Paulo,SP).



