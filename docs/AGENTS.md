# 📊 Agentes de Monitoramento

## 🤖 Como Funciona o Sistema Multi-Agente

O Atena usa 3 agentes principais que trabalham em **círculos independentes** mas se comunicam através do **Oracle** (supervisor).

```
┌─────────────────────────────────────────────────────────────────┐
│                    SISTEMA MULTI-AGENTE                          │
│                                                                  │
│                        ┌──────────────┐                         │
│                        │  👁️ ORACLE   │                         │
│                        │  (Supervisor) │                         │
│                        └──────┬───────┘                         │
│                               │                                  │
│           ┌───────────────────┼───────────────────┐             │
│           ▼                   ▼                   ▼             │
│    ┌──────────┐      ┌──────────────┐    ┌──────────────┐      │
│    │ 👻 HUNTER│      │ 🛡️ CYBERGUARD│    │ 📝 CONTEÚDO  │      │
│    │ Tecnologia│      │  Segurança   │    │  Roteiros    │      │
│    └──────────┘      └──────────────┘    └──────────────┘      │
│                                                                  │
│  Cada agente é INDEPENDENTE: se um falha, os outros continuam   │
└─────────────────────────────────────────────────────────────────┘
```

---

## 👻 Hunter — System Hunter

### Identidade
**Nome:** Hunter Atena  
**Apelido:** 👻 Fantasma  
**Missão:** Caçar novas tecnologias, melhorias de arquitetura e oportunidades free tier 24/7

### Escopo
- **Foco:** 100% técnico — sem fofocas de mercado
- **Autonomia:** Pode aplicar melhorias sem permissão
- **Formato:** Relatórios em hunter/surface/YYYY-MM-DD-{tipo}.md

### Turnos Detalhados

#### 🌅 Turno 1 — 06:00 (Caçada Pesada)
```
🔍 Varredura inicial de TODOS os serviços
├── Lista ferramentas novas
├── Verifica atualizações disponíveis
├── Checa status de cada serviço
└── Gera relatório com "🔥 Descoberta Quente"
```

#### 🌤️ Turno 2 — 12:00 (Deep Doc)
```
📚 Documentação técnica aprofundada
├── Pega a ferramenta mais promissora do turno 1
├── Lê documentação completa
├── Analisa viabilidade técnica
└── Gera relatório de recomendação
```

#### 🌙 Turno 3 — 18:00 (Vigilância)
```
👁️ Status check de serviços já integrados
├── SnapDeploy 🟢/🔴
├── NVIDIA NIM 🟢/🔴
├── Postiz 🟢/🔴
├── n8n CE 🟢/🔴
├── Supabase 🟢/🔴
├── Cloudflare 🟢/🔴
└── Kaggle 🟢/🔴
```

---

## 🛡️ CyberGuard — Guardião de Segurança

### Identidade
**Nome:** CyberGuard  
**Apelido:** 🛡️ Escudo  
**Missão:** Monitorar ameaças, portas, processos e conexões 24/7

### Sub-agentes

#### 📡 Port Scanner
- Escaneia portas abertas no sistema
- Compara com baseline de portas conhecidas
- Alerta se encontrar porta desconhecida

#### 🕵️ Threat Monitor
- Analisa processos em execução
- Detecta padrões suspeitos
- Verifica integridade de arquivos do sistema

#### 🔐 Firewall Check
- Verifica regras de firewall
- Testa exposição de serviços
- Valida configurações de rede

#### 🔌 Conexões Ativas
- Lista conexões estabelecidas
- Identifica IPs suspeitos
- Monitora tráfego anômalo

---

## 👁️ Oracle — Supervisor Central

### Identidade
**Nome:** Oracle  
**Apelido:** 👁️ O Olho  
**Missão:** Coletar, validar e consolidar relatórios de todos os agentes

### Fluxo de Supervisão

```
1. Recebe relatório do Hunter → valida → salva
2. Recebe relatório do CyberGuard → valida → salva
3. Gera resumo geral do turno
4. Salva no repositório
5. Se crítico → notifica via WhatsApp
6. Se tudo ok → confirma silenciosamente
```

### Matriz de Decisão

| Estado | Condição | Ação |
|--------|----------|------|
| 🟢 Tudo ok | Sem alertas, sem erros | "Todos os agentes operacionais" |
| 🟡 Atenção | Alerta menor, 1 serviço instável | "Atenção: [problema]" |
| 🔴 Crítico | Serviço fora do ar, ameaça real | "🚨 Emergência: [problema]" + WhatsApp |