# 🌌 ATENA ECOSYSTEM

> **Sistema de Agentes e Automação Inteligente**
> Unindo Design, Tecnologia e IA para criar conteúdo e monitorar infraestrutura — tudo de graça, tudo na nuvem.

---

## 📋 Índice

- [🏗️ Arquitetura Geral](docs/ARCHITECTURE.md)
- [🧩 Componentes do Sistema](docs/COMPONENTS.md)
- [🔄 Workflows e Automações](docs/WORKFLOWS.md)
- [📊 Agentes de Monitoramento](docs/AGENTS.md)
- [🎨 Design System](docs/DESIGN_SYSTEM.md)
- [📱 Fluxo de Conteúdo](docs/CONTENT_PIPELINE.md)
- [⚙️ Infraestrutura Técnica](docs/INFRASTRUCTURE.md)

---

## 🎯 Visão Geral

O **Atena Ecosystem** é um sistema modular de **agentes inteligentes** e **automações** que funciona 100% na nuvem usando serviços gratuitos. O celular é apenas uma **tela burra** — tudo que é pesado roda na nuvem.

### Pilares

| Pilar | O que faz | Tecnologia |
|-------|-----------|------------|
| 🧠 **Zapia** | Assistente central, orquestrador de skills | Zapia + Skills |
| 👻 **Hunter** | Caça de tecnologias 24/7, 3 turnos/dia | Zapia Cron |
| 🛡️ **CyberGuard** | Monitoramento de segurança | Zapia Cron |
| 👁️ **Oracle** | Supervisor dos agentes, resumo geral | Zapia Cron |
| 🎨 **Design** | Criação visual assistida por IA | Cloudflare + Airtable |
| 📱 **Conteúdo** | Roteiros diários para clientes | Zapia Cron + Airtable |
| ⚙️ **Infra** | Servidores, bancos, storage | Render + Cloudflare |

---

## 🏗️ Como Está Estruturado

```
                    ☁️ NUVEM (processamento pesado)
         ┌──────────────────────────────────────────────┐
         │                                              │
         │   🧠 ZAPIA (Cérebro Central)                 │
         │   ├── Skills (módulos)                       │
         │   │   ├── airtable       → CRUD clientes     │
         │   │   ├── cloudflare-ai  → Imagens via FLUX  │
         │   │   ├── nvidia-nim     → LLMs grátis       │
         │   │   ├── copy-angel     → Copywriting       │
         │   │   ├── design-angel   → Design visual     │
         │   │   └── hunter-angelos → Scout tecnológico │
         │   │                                            │
         │   ├── Agentes (Cron)                          │
         │   │   ├── 👻 Hunter (6h/12h/18h)              │
         │   │   ├── 🛡️ CyberGuard (6h/12h/18h)         │
         │   │   └── 👁️ Oracle (pós-agentes)             │
         │   │                                            │
         │   ├── Automações (Cron)                       │
         │   │   ├── Roteiros Dra. Luísa  → 23h diário  │
         │   │   ├── Roteiros Dr. Luciano → Sáb 8h      │
         │   │   ├── Roteiros Angel Sakura → Sáb 9h    │
         │   │   └── Limpeza de e-mail   → 08:30 seg-sex │
         │   │                                            │
         │   └── 📊 Dashboard Atena                      │
         │       └── Mini-Canva + Analytics + Estúdio    │
         │                                                │
         └────────────┬─────────────────────────────────┘
                      │
         ┌────────────┴────────────┐
         │   📱 POCO C65           │
         │   Tela Burra            │
         │   Só transmite/recebe   │
         └─────────────────────────┘
```

---

## 🚀 Tecnologias Usadas

| Serviço | Plano | O que faz |
|---------|-------|-----------|
| **Zapia** | Free | Assistente central + skills + crons |
| **Airtable** | Free | Banco de dados de clientes e roteiros |
| **Cloudflare Workers** | Free | Geração de imagens (FLUX, SDXL, Dreamshaper) |
| **Cloudflare R2** | Free (10GB) | Armazenamento de arquivos |
| **NVIDIA NIM** | Free | LLMs (Mistral, Qwen, Llama) |
| **Render** | Free | n8n + FreeLLMAPI + Dashboard |
| **GitHub** | Free | Código fonte, portfólio, deploy |
| **WhatsApp** | — | Canal de comunicação com a usuária |

---

## 📊 Status Geral

| Componente | Status |
|------------|--------|
| 🧠 Zapia + Skills | 🟢 100% operacional |
| 👻 Hunter (3 turnos) | 🟢 24/7 ativo |
| 🛡️ CyberGuard | 🟢 24/7 ativo |
| 👁️ Oracle | 🟢 Pós-agentes |
| 🎨 Geração de Imagens | 🟢 Cloudflare FLUX |
| 📱 Roteiros Clientes | 🟢 Automatizado |
| 📊 Dashboard Atena | 🟢 Online |
| 💾 Airtable | 🟢 Conectado |
| 🗄️ Supabase | ⏳ Aguardando login |

---

## 🧭 Progresso

```
🧠 Design Visual   ██████████░░░░  70%  (skills criadas)
🤖 Agentes         ████████████░░  80%  (3 agentes ativos)
📊 Dados           ██████████░░░░  60%  (Airtable OK)
📱 Conteúdo        ██████████████  85%  (roteiros automatizados)
🌐 Infraestrutura  ██████████░░░░  65%  (free tier)
⚙️ Dashboard       ██████████░░░░  70%  (funcional)
🏁 **GERAL**       ███████████░░░   **72%**
```

---

## 👤 Sobre

Criado para **Jessica Gaya** — Social Media, Designer e futura profissional híbrida em Design + Tecnologia.

> _"Unir Social Media e Design com Automação e Análise de Dados — não largar uma área pela outra, mas ser a profissional híbrida que entende de tecnologia E de comunicação visual."_

---

📅 **Última atualização:** 2026-07-24