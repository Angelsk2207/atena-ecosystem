# 🔄 Workflows e Automações

## Visão Geral

Todas as automações rodam como **crons do Zapia** — não precisam de servidor extra, não gastam recursos, são agendadas e executadas automaticamente.

---

## 📋 Lista de Crons Ativos

### Automações de Conteúdo

| Nome | Horário | Frequência | O que faz |
|------|---------|------------|-----------|
| 📝 **Roteiros Dra. Luísa** | 23:00 | Diário | Gera 3 roteiros de Direito Criminal |
| 📝 **Roteiros Dr. Luciano** | 08:00 Sáb | Semanal | Gera 3 roteiros de Direito Civil |
| 📝 **Roteiros Angel Sakura** | 09:00 Sáb | Semanal | Gera 3 roteiros de Design+Tech |
| 📧 **Limpeza de E-mail** | 08:30 seg-sex | Dias úteis | Revisa e organiza caixa de entrada |

### Agentes de Monitoramento

| Nome | Horário | Frequência | O que faz |
|------|---------|------------|-----------|
| 👻 **Hunter Turno 1** | 06:00 | Diário | Caçada Pesada de novas tecnologias |
| 👻 **Hunter Turno 2** | 12:00 | Diário | Deep Doc de ferramentas |
| 👻 **Hunter Turno 3** | 18:00 | Diário | Vigilância de serviços |
| 🛡️ **CyberGuard Turno 1** | 06:00 | Diário | Port Scan + Threat Monitor |
| 🛡️ **CyberGuard Turno 2** | 12:00 | Diário | Firewall Check + Conexões |
| 🛡️ **CyberGuard Turno 3** | 18:00 | Diário | Scan completo |
| 👁️ **Oracle pós-agentes** | Após cada | Diário | Supervisor, consolida relatórios |

---

## 🔄 Fluxo de Cada Automação

### Fluxo de Roteiros (Ex: Dra. Luísa)

```
┌─────────────────────────────────────────────────────────────────┐
│                    ROTEIROS DR. LUÍSA                            │
│                                                                  │
│  ⏰ 23:00 → Cron dispara                                       │
│    ↓                                                             │
│  🧠 Zapia consulta Airtable (preferências da cliente)           │
│    ↓                                                             │
│  ✍️ Gera 3 roteiros:                                            │
│    ├── Manhã: Story sobre notícia criminal em alta              │
│    ├── 12h: Story chamando Reel 15h                             │
│    └── 18h: Story chamando Reel 20:30                           │
│    ↓                                                             │
│  💾 Salva no Airtable (tabela Roteiros)                         │
│    ↓                                                             │
│  📱 Envia pelo WhatsApp: "Roteiros Luísa prontos:"              │
│    ├── ✅ Roteiro 1: [tema]                                      │
│    ├── ✅ Roteiro 2: [tema]                                      │
│    └── ✅ Roteiro 3: [tema]                                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Fluxo Hunter (Ex: Turno 1 — 06:00)

```
┌─────────────────────────────────────────────────────────────────┐
│                    HUNTER TURNO 1 (06:00)                        │
│                                                                  │
│  ⏰ 06:00 → Cron dispara                                       │
│    ↓                                                             │
│  🔍 Varredura de novas ferramentas:                             │
│    ├── SnapDeploy → status do free tier                         │
│    ├── NVIDIA NIM → RPM atual                                   │
│    ├── Postiz → stars e commits                                 │
│    ├── n8n CE → versão                                          │
│    ├── Supabase → free tier                                     │
│    ├── Cloudflare → Workers/R2                                  │
│    └── Kaggle → GPU horas/semana                                │
│    ↓                                                             │
│  📊 Gera relatório em hunter/surface/YYYY-MM-DD-cacada.md       │
│    ↓                                                             │
│  🔥 Se encontrar algo novo: destaca como "Descoberta Quente"    │
│    ↓                                                             │
│  🛠️ Se for melhoria de arquitetura: aplica automaticamente      │
│    ↓                                                             │
│  📱 Envia resumo via WhatsApp                                   │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

### Fluxo Oracle (Pós-agentes)

```
┌─────────────────────────────────────────────────────────────────┐
│                    ORACLE — SUPERVISOR                           │
│                                                                  │
│  📥 Recebe relatório do Hunter                                  │
│    ↓                                                             │
│  📥 Recebe relatório do CyberGuard                              │
│    ↓                                                             │
│  🔍 Valida cada relatório:                                      │
│    ├── 🟢 Tudo ok → "Todos os agentes operacionais"             │
│    ├── 🟡 Alerta → "Atenção: [problema]"                        │
│    └── 🔴 Crítico → "🚨 Emergência: [problema]" + notifica      │
│    ↓                                                             │
│  💾 Salva supervisão em agents/oracle/reports/                  │
│    ↓                                                             │
│  📱 Se crítico: envia alerta urgente via WhatsApp               │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📅 Calendário Semanal de Automações

```
        SEG        TER        QUA        QUI        SEX        SÁB        DOM
06:00  ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─
       ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─
08:00  │                                                                          
08:30  │ 📧Email                                                                   
12:00  ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─
       ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─
18:00  ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─ ─ Hunter ─
       ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─ ─ Cyber  ─
20:00  │                                                 ┌ Luciano ┐               
23:00  ─ Luísa ─ ─ Luísa ─ ─ Luísa ─ ─ Luísa ─ ─ Luísa ─ ──────── ─ ──────── ─
                                                          ┌ Angel  ─              
                                                          └ Sakura ─              
```

---

## 🛠️ Workflows Futuros (Planejados)

| Workflow | Status | Descrição |
|----------|--------|-----------|
| 📱 Postagem automática em redes | ⏳ Pendente | Conectar Instagram/Facebook/TikTok |
| 📊 Dashboard de métricas | ⏳ Pendente | Analytics integrado no Dashboard Atena |
| 📧 Captura de leads automática | ⏳ Pendente | Responder comentários + salvar contato |
| 🔄 Dupla escrita Airtable+Supabase | ⏳ Pendente | Redundância de dados |