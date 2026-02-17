📧 Automation of Gmail Summarization (n8n Workflow)
This project is an AI-powered Gmail automation workflow built using n8n, OpenAI, Gmail API, and Telegram Bot API.
The workflow allows users to:

**1️⃣ Telegram Trigger Node**

Node Type: n8n-nodes-base.telegramTrigger

**🔹 Purpose**

Acts as the entry point of the workflow by listening for incoming Telegram messages.

****🔹 Function

Receives user commands

Extracts:

message.text

message.chat.id

Passes user input to the AI Agent

🔹 Authentication Required

Telegram Bot API Token

**2️⃣ AI Agent Node (LangChain Agent)
**
Node Type: @n8n/n8n-nodes-langchain.agent

**🔹 Purpose**

Acts as the decision-making engine of the workflow.

**🔹 Responsibilities**

Interprets user instructions

Determines whether to:

Summarize emails

Send emails

Summarize and send

Generates a structured execution report

Communicates with connected tools (Gmail + OpenAI)

🔹 Special Configuration

Uses a strict system prompt

Enforces structured output format

Returns only execution report (no extra text)

**3️⃣ OpenAI Chat Model Node**

Node Type: @n8n/n8n-nodes-langchain.lmChatOpenAi

🔹 Purpose

Provides Large Language Model (LLM) capabilities.

🔹 Function

Processes user requests

Summarizes email content

Generates execution report

Connected to AI Agent via ai_languageModel

🔹 Model Used

gpt-5-mini (configurable)

🔹 Authentication Required

OpenAI API Key

**4️⃣ Gmail Tool Node (Get Many Messages)**

Node Type: n8n-nodes-base.gmailTool

🔹 Operation Used

getAll

🔹 Purpose

Retrieves multiple emails from Gmail inbox.

🔹 Function

Fetches email data

Sends email content to AI Agent

Allows AI to summarize messages

🔹 Authentication Required

Gmail OAuth2 Credential

**5️⃣ Telegram Send Message Node**

Node Type: n8n-nodes-base.telegram

🔹 Purpose

Sends the final execution report back to the Telegram user.

🔹 Configuration

Chat ID dynamically extracted from Telegram Trigger

Sends AI-generated report

**🔄 Tool Interaction Flow**
Telegram Trigger
        ↓
AI Agent
        ↙        ↘
OpenAI Model   Gmail Tool
        ↓
Telegram Send Message

🔐 Credential Dependencies
Tool	Credential Required
Telegram Trigger	Telegram Bot Token
OpenAI Model	OpenAI API Key
Gmail Tool	Gmail OAuth2
Telegram Send	Telegram Bot Token
