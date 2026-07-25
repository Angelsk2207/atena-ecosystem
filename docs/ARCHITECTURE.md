# 🏗️ Arquitetura Geral do Ecossistema Atena

## Filosofia Central: PESO ZERO

> **POCO C85** vira **tela burra**. Tudo que é pesado roda em **5 nuvens simultâneas**.
> Logs e dados são duplicados entre **Airtable e Supabase** pra nunca perder nada.

---

## 🌐 Diagrama de Arquitetura

```
╔══════════════════════════════════════════════════════════════════════════╗
║                          📱 POCO C85 — TELA BURRA                       ║
║                                                                          ║
║  ┌──────────────────────────────────────────────────────────────────┐   ║
║  │  🟢 WhatsApp (comandos de voz/áudio → Zapia)                    │   ║
║  │  🟢 Termux (só mantém túnel ativo, não processa nada)           │   ║
║  │  🔴 NADA de processamento pesado aqui                           │   ║
║  └──────────────────────────────────────────────────────────────────┘   ║
║                                    │                                      ║
║                                    ▼                                      ║
╚══════════════════════════════════════════════════════════════════════════════╝
                                    │
                                    ▼
╔══════════════════════════════════════════════════════════════════════════╗
║                          🧠 ZAPIA — CÉREBRO CENTRAL                     ║
║                                                                          ║
║  ┌──────────────────────────────────────────────────────────────────┐   ║
║  │  ▶️ Interpreta comandos                                          │   ║
║  │  ▶️ Escolhe a skill certa (Airtable, Cloudflare, NVIDIA...)     │   ║
║  │  ▶️ Agenda automações (31 crons ativos)                         │   ║
║  │  ▶️ Gerencia agentes (Hunter, CyberGuard, Oracle)               │   ║
║  │  ▶️ Entrega resultados no WhatsApp                              │   ║
║  └──────────────────────────────────────────────────────────────────┘   ║
║                                    │                                      ║
║          ┌─────────────────────────┼─────────────────────────┐          ║
║          ▼                         ▼                         ▼          ║
║     🎨 Skills                 🤖 Agentes              ☁️ 5 Nuvens      ║
╚══════════════════════════════════════════════════════════════════════════╝
                                    │
                                    ▼
╔══════════════════════════════════════════════════════════════════════════╗
║                     ☁️ AS 5 NUVENS (Free Tier)                          ║
║                                                                          ║
║  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌────────────┐  ║
║  │  1. RENDER   │  │ 2. CLOUDFLARE│  │  3. KOYEB    │  │4. SNAPDEPLOY║
║  │              │  │              │  │              │  │            │  ║
║  │ n8n          │  │ Workers AI   │  │ Backup n8n   │  │ Deploys    │  ║
║  │ FreeLLMAPI   │  │ R2 Storage   │  │ Backup LLMAPI│  │ rápidos    │  ║
║  │ Dashboard    │  │ FLUX/SDXL    │  │              │  │            │  ║
║  └──────────────┘  └──────────────┘  └──────────────┘  └────────────┘  ║
║                                  ┌──────────────┐                       ║
║                                  │  5. ZEABUR   │                       ║
║                                  │              │                       ║
║                                  │ Redundância  │                       ║
║                                  │ extra        │                       ║
║                                  └──────────────┘                       ║
╚══════════════════════════════════════════════════════════════════════════╝
                                    │
                                    ▼
╔══════════════════════════════════════════════════════════════════════════╗
║                     🗄️ LOGS E DADOS (Dupla Escrita)                    ║
║                                                                          ║
║  ┌──────────────────────────────────────────────────────────────────┐   ║
║  │  📊 AIRTABLE (já funcionando)                                   │   ║
║  │     → Clientes, roteiros, relatórios dos agentes, cache         │   ║
║  │                                                                  │   ║
║  │  🗄️ SUPABASE (em implementação)                                 │   ║
║  │     → Backup de TUDO que está no Airtable                       │   ║
║  │     → Se Airtable cair, Supabase assume                         │   ║
║  └──────────────────────────────────────────────────────────────────┘   ║
║                                    │                                      ║
║                                    ▼                                      ║
║                     🐙 GitHub Público (Código)                          ║
╚══════════════════════════════════════════════════════════════════════════╝
```

---

## 🔄 Fluxo de Funcionamento

### 1️⃣ Você Fala
```
Jessica: "Zapia, cria roteiro da Luísa sobre [tema]"
   │
   ▼
WhatsApp → Zapia (nuvem) → interpreta áudio
```

### 2️⃣ Zapia Processa
```
Zapia entende → escolhe a skill certa
   │
   ├── copy-angel → escreve roteiro
   ├── airtable → salva log
   └── cloudflare-ai → gera imagem se precisar
```

### 3️⃣ Resultado Volta
```
Roteiro pronto → salvo no Airtable → log duplicado no Supabase
   │
   ▼
WhatsApp: "Pronto! Aqui estão os 3 roteiros da Luísa 📝"
```

---

## 🔄 Fluxo dos Agentes (24/7)

```
            ┌──────────────────┐
            │  👻 HUNTER       │ ← Caça tecnologias (06h/12h/18h)
            │  Tecnologia      │
            └──────┬───────────┘
                   │ relatório
                   ▼
┌──────────────────┬──────────────────┐
│  🛡️ CYBERGUARD  │                  │
│  Segurança      │   👁️ ORACLE      │ ← Supervisor
│  (06h/12h/18h)  │   Coleta tudo    │
└──────┬───────────┘   Gera resumo    │
       │ relatório     Alerta se      │
       └─────────────── crítico       │
                      └──────┬────────┘
                             │
                ┌────────────┼────────────┐
                ▼            ▼            ▼
           Airtable     Supabase    WhatsApp (se crítico)
```

---

## 🛡️ Tolerância a Falhas

| Cenário | O que acontece |
|---------|---------------|
| Render cai | Koyeb assume |
| Koyeb cai | Zeabur assume |
| Cloudflare cai | NVIDIA NIM (texto) ainda funciona |
| Airtable cai | Supabase mantém os dados |
| Supabase cai | Airtable mantém os dados |
| POCO C85 desliga | Nada — ele só transmite, nuvem continua |

---

## 📊 Componentes por Nuvem

| Nuvem | Serviço | Função | Status |
|-------|---------|--------|--------|
| ☁️ Render | n8n | Orquestrador de workflows | 🟢 |
| ☁️ Render | FreeLLMAPI | 69 modelos de IA (proxy) | 🟢 |
| ☁️ Render | Dashboard Atena | Painel de controle | 🟢 |
| ☁️ Cloudflare | Workers AI | Geração de imagem (FLUX, SDXL) | 🟢 |
| ☁️ Cloudflare | R2 | Armazenamento (10GB free) | 🟢 |
| ☁️ Cloudflare | Tunnel | Conexão segura sem IP exposto | 🟢 |
| ☁️ Koyeb | Backup n8n | Redundância do Render | ⏳ |
| ☁️ SnapDeploy | Deploys rápidos | Testes e protótipos | ⏳ |
| ☁️ Zeabur | Redundância extra | Última camada de fallback | ⏳ |
| 🗄️ Airtable | Banco principal | Dados ativos | 🟢 |
| 🗄️ Supabase | Banco secundário | Backup e redundância | 🔄 |