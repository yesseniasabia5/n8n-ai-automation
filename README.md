# 🤖 n8n AI Automation Projects

> Production-ready multi-agent automation systems built on n8n, integrating LLMs, WhatsApp, Jira, Google Drive and more through a custom MCP client/server architecture.

![n8n](https://img.shields.io/badge/n8n-workflow-orange?logo=n8n)
![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Azure OpenAI](https://img.shields.io/badge/Azure-OpenAI-0078D4?logo=microsoft-azure)
![LangChain](https://img.shields.io/badge/LangChain-agent-green)
![WhatsApp](https://img.shields.io/badge/WhatsApp-API-25D366?logo=whatsapp)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## 📁 Projects

- [Bot Skyner](#-bot-skyner) — WhatsApp AI assistant with voice transcription and LLM agent
- [Workers](#-workers) — Multi-agent supervisor system with Slack, Jira, Drive and database integrations

---

## 🔵 Bot Skyner

### Why I built this

I needed a WhatsApp-native AI assistant that could handle both text and voice messages, route them through an LLM agent with memory, and connect to business tools like Airtable and Gmail — all without a custom backend. Built entirely on n8n using a custom MCP client/server pattern for real-time communication.

### What it does

- Receives text and voice messages from WhatsApp
- Downloads audio and transcribes it via **AssemblyAI**
- Processes the transcript through an **LLM agent (OpenRouter)** with persistent memory via n8n LangChain nodes
- Connects to **Airtable** for data lookups and **Gmail** for notifications
- Sends responses back via WhatsApp API
- Uses a custom **MCP (client/server) over SSE** for real-time inter-workflow communication

### Screenshot
![Bot Skyner Client workflow](Bot Skynet/img/Screenshot_client.png)

![Bot Skyner Server workflow](Bot Skynet/img/Screenshot_server.png)

### Architecture

```mermaid
flowchart LR
    A[User on WhatsApp] --> B[WhatsApp Trigger]
    B --> C[Download audio / get message]
    C --> D[AssemblyAI upload & transcribe]
    D --> E[Transcription text]
    E --> F[LLM Agent OpenRouter + Memory]
    F --> G[MCP Client SSE]
    G --> H[MCP Server]
    H --> I[Airtable]
    H --> J[Gmail]
    F --> K[WhatsApp API - Send Message]
    H --> K
```

### Tech stack

| Layer | Technology |
|---|---|
| Workflow engine | n8n |
| Voice transcription | AssemblyAI |
| LLM / Agent | OpenRouter (via LangChain nodes) |
| Messaging | WhatsApp Business API |
| Data | Airtable |
| Notifications | Gmail OAuth |
| Real-time comms | MCP over SSE / webhooks |

### Files

| File | Description |
|---|---|
| `MCP Client Skynet.json` | Client workflow — WhatsApp trigger, transcription, LLM, response |
| `MCP Server Skynet.json` | Server workflow — Airtable, Gmail, MCP trigger |
| `secrets template.txt` | Variable name template for manual environment setup |

---
