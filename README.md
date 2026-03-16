# 🌤️ Telegram Weather Chatbot - Desafio N8N

Este projeto consiste em um chatbot automatizado para o Telegram, desenvolvido utilizando a ferramenta **N8N**. O objetivo principal é informar a temperatura atual de qualquer cidade do Brasil em tempo real, utilizando a API do **OpenWeather**.

---

## 🚀 Funcionalidades

* **Interatividade:** Recebe mensagens de texto via Telegram.
* **Processamento:** Normaliza nomes de cidades (ajuste de espaços e caracteres).
* **Integração:** Consulta dados meteorológicos globais via API REST.
* **Validação:** Sistema de tratamento de erros para cidades não encontradas.
* **Feedback Visual:** Respostas claras com emojis e temperaturas arredondadas.

---

## 📋 Pré-requisitos

Para rodar este chatbot, você precisará de:

1. **N8N:** Instância rodando localmente (Docker/Desktop) ou Cloud.
2. **Telegram Bot Token:** Criado através do bot [@BotFather](https://t.me/botfather).
3. **OpenWeather API Key:** Chave gratuita obtida em [OpenWeatherMap](https://openweathermap.org/).

---

## 📥 Como Importar o Workflow

1. Baixe o arquivo `workflow-chatbot-telegram.json` deste repositório.
2. No seu painel do **N8N**, clique no menu superior e selecione **Import from File**.
3. Escolha o arquivo JSON baixado.
4. Clique em **Save** no canto superior direito.

---

## 🔑 Configuração de Credenciais

Após importar, você deve configurar as credenciais no N8N para que os nós funcionem:

### 1. Telegram (Telegram API)
* No menu lateral, vá em **Credentials** > **Add Credential**.
* Procure por **Telegram API**.
* Insira o seu `TELEGRAM_BOT_TOKEN`.

### 2. OpenWeather (Variável de Ambiente)
* No menu lateral, vá em **Credentials** > **Add Credential**.
* Procure por **OpenWeatherMap API**.
* Insira a sua `OPENWEATHER_API_KEY`.
  O nó de http já está configurado com a autenticação pela credencial da OpenWeatherMap.

---

## 🛠️ Estrutura do Workflow

O fluxo segue os requisitos técnicos obrigatórios:

1. **Telegram Trigger:** Detecta novas mensagens de texto.
2. **Set Node (`queue`):** Captura e limpa o texto enviado pelo usuário.
3. **HTTP Request:** Consulta o endpoint oficial da OpenWeather com os parâmetros `units=metric` (graus celsius) e `lang=pt_br`.
4. **IF Node:** Verifica se a cidade foi encontrada (Status 200).
5. **Telegram Send Message:** * **Sucesso:** Retorna a temperatura formatada (ex: `25°C`).
    * **Erro:** Retorna uma mensagem de orientação caso a cidade seja inválida.

---

## 🧪 Como Executar e Testar

1. No N8N, clique no botão **Execute Workflow**.
2. Abra o Telegram e procure pelo seu bot.
3. Envie o nome de uma cidade (Exemplo: `São Paulo`).
4. **Retorno esperado:** `🌤️ A temperatura em São Paulo é de 22°C.`
5. **Teste de Erro:** Envie um nome inexistente para validar a mensagem de erro: `❌ Cidade não encontrada.`

---

## ⚠️ Segurança

> **Importante:** O arquivo `workflow-chatbot-telegram.json` exportado não contém tokens reais. Nunca suba suas chaves privadas para repositórios públicos.

---
*Desenvolvido para fins de desafio técnico em automação.*
