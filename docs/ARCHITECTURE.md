# 🏗️ Arquitetura Geral do Ecossistema Atena

## Filosofia Central

> **"Peso Zero"** — Tudo que é pesado roda na nuvem. O celular (POCO C65) é apenas uma interface de transmissão.
> O cérebro é o Zapia + Skills, que orquestra tudo.

---

## 🌐 Diagrama de Arquitetura

```
╔══════════════════════════════════════════════════════════════════╗
║                    ☁️ NUVEM (Render + Cloudflare)               ║
║                                                                  ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │               🧠 ZAPIA (Cérebro Central)                 │   ║
║  │  ┌──────────┬──────────┬──────────┬──────────────────┐   │   ║
║  │  │ SKILLS   │  AGENTES │ AUTOMAÇÕES│ DASHBOARD ATENA │   │   ║
║  │  │ (Módulos)│  (Cron)  │  (Cron)   │ (Visual)        │   │   ║
║  │  └──────────┴──────────┴──────────┴──────────────────┘   │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  ┌───────────────┐  ┌───────────────┐  ┌───────────────────┐   ║
║  │ Cloudflare    │  │  NVIDIA NIM   │  │  Airtable         │   ║
║  │ Workers AI    │  │  LLMs grátis  │  │  Banco de Dados   │   ║
║  │ (FLUX, SDXL)  │  │ (Mistral, etc)│  │ (Clientes, Rots)  │   ║
║  └───────┬───────┘  └───────┬───────┘  └────────┬──────────┘   ║
║          │                  │                    │               ║
║          └──────────────────┴────────────────────┘               ║
║                             │                                    ║
║                    ┌────────┴────────┐                           ║
║                    │  Render (n8n)   │                           ║
║                    │  (FreeLLMAPI)   │                           ║
║                    └─────────────────┘                           ║
╚══════════════════════════════════════════════════════════════════╝
                              │
                              ▼
╔══════════════════════════════════════════════════════════════════╗
║                  📱 POCO C65 (Tela Burra)                       ║
║                                                                  ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  📲 WhatsApp ← canal principal de comunicação            │   ║
║  │  Áudio → Zapia processa → entrega via WhatsApp          │   ║
║  │  Tudo que é pesado fica na nuvem                        │   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                  ║
║  RAM: 4-8GB (buffer de transmissão)                             ║
║  CPU: Helio G85 (só mantém terminal)                            ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 🔄 Fluxo de Processamento

### Como cada ação flui do comando à execução

```
┌─────────────────────────────────────────────────────────────────┐
│                    FLUXO PRINCIPAL                               │
│                                                                  │
│  📱 Jessica fala                                                │
│    ↓                                                             │
│  🎤 Áudio chega no Zapia                                        │
│    ↓                                                             │
│  🧠 Zapia interpreta o pedido (processamento na nuvem)          │
│    ↓                                                             │
│  🔍 Escolhe a Skill certa:                                      │
│    ├── **airtable** → CRUD no banco de dados                    │
│    ├── **cloudflare-ai** → gera imagem                          │
│    ├── **nvidia-nim** → consulta LLM                            │
│    ├── **copy-angel** → escreve roteiro/texto                   │
│    ├── **design-angel** → pesquisa referências + gera imagem    │
│    ├── **hunter-angelos** → varre novas tecnologias             │
│    └── **agentes cron** → execução automática programada        │
│    ↓                                                             │
│  ✅ Resposta volta pro WhatsApp da Jessica                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🧩 Distribuição dos Agentes em Turnos

```
                    ╔════════════════════════╗
                    ║     LINHA DO TEMPO     ║
                    ╚════════════════════════╝

🌅 06:00 ─── 👻 HUNTER Turno 1 (Caçada Pesada)
                 🛡️ CYBERGUARD Turno 1 (Port Scan + Threat)

🌤️ 12:00 ─── 👻 HUNTER Turno 2 (Deep Doc)
                 🛡️ CYBERGUARD Turno 2 (Firewall + Conexões)

🌙 18:00 ─── 👻 HUNTER Turno 3 (Vigilância)
                 🛡️ CYBERGUARD Turno 3 (Completo)

🌃 Após cada ── 👁️ ORACLE (Supervisor: coleta + resume)

📅 Diário ─── 08:30 → Limpeza de e-mail (seg-sex)
                23:00 → Roteiros Dra. Luísa

📅 Semanal ── Sáb 08:00 → Roteiros Dr. Luciano
                 Sáb 09:00 → Roteiros Angel Sakura
```

---

## 🗂️ Estrutura de Dados

```
                    ┌──────────────────────────┐
                    │      AIRTABLE            │
                    │   (Banco principal)      │
                    │                          │
                    │  📋 Tabela: Clientes     │
                    │  ├── Nome                │
                    │  ├── Tipo de conteúdo    │
                    │  ├── Formato             │
                    │  └── Horários            │
                    │                          │
                    │  📋 Tabela: Roteiros     │
                    │  ├── Cliente (FK)        │
                    │  ├── Data                │
                    │  ├── Turno (manhã/12h/18h)│
                    │  └── Conteúdo            │
                    │                          │
                    │  📋 Tabela: Skill Cache  │
                    │  └── Dados temporários   │
                    └──────────────────────────┘
```

---

## 🛡️ Segurança e Tolerância a Falhas

```
┌─────────────────────────────────────────────────────────────────┐
│                    TOLERÂNCIA A FALHAS                           │
│                                                                  │
│  🔴 Se Hunter falhar → CyberGuard continua → Oracle avisa       │
│  🔴 Se CyberGuard falhar → Hunter continua → Oracle avisa       │
│  🔴 Se Oracle falhar → Agentes rodam sem supervisão             │
│  🔴 Se Airtable cair → Dados ainda em cache local               │
│  🔴 Se Render cair → Koyeb/Zeabur/SnapDeploy assumem            │
│                                                                  │
│  🟢 Múltiplos provedores de nuvem = zero downtime               │
│  🟢 Cada agente é independente = falha isolada                  │
│  🟢 Dados no Airtable, não no servidor = dados seguros          │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🎯 Princípios de Design da Arquitetura

1. **Peso Zero** — Celular só transmite, nuvem processa
2. **Modular** — Cada skill/agente é independente
3. **Auto-evolutivo** — Hunter encontra melhorias, aplica sem permissão
4. **Free Tier First** — Tudo dentro do plano gratuito
5. **Documentado** — Cada peça tem seu documento de referência
6. **Resiliente** — Múltiplas nuvens, tolerância a falhas
7. **Foco em áudio** — Jessica fala, Zapia processa, WhatsApp entrega