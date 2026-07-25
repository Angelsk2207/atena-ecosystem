# 🤖 Agentes de Monitoramento — 24/7

## Como Funciona o Sistema Multi-Agente

O Atena usa 3 agentes que **trabalham em círculos independentes**, mas se comunicam através do **Oracle** (supervisor). Logs de TODOS os agentes vão para **Airtable + Supabase** (dupla escrita).

---

## 🔄 Fluxo de Comunicação entre Agentes

```
                    ┌──────────────────────────────────────────────────┐
                    │              👁️ ORACLE (Supervisor)              │
                    │                                                  │
                    │  Coleta relatórios → Valida → Gera resumo        │
                    │  Salva no Airtable → Salva no Supabase           │
                    │  Se crítico → Alerta no WhatsApp                 │
                    └──────┬────────────────────────────────┬──────────┘
                           │                                │
           ┌───────────────┼────────────────┐               │
           ▼               ▼                ▼               │
    ┌──────────┐   ┌──────────────┐   ┌──────────┐         │
    │ 👻 HUNTER│   │ 🛡️ CYBERGUARD│   │ 📝 CONTEÚDO│       │
    │ Tecnologia│   │  Segurança   │   │  Roteiros  │       │
    └──────────┘   └──────────────┘   └──────────┘         │
           │               │                │               │
           ▼               ▼                ▼               │
    ┌──────────────────────────────────────────────────┐    │
    │           🗄️ Logs (Airtable + Supabase)          │◄───┘
    └──────────────────────────────────────────────────┘

Cada agente é INDEPENDENTE: se um falha, os outros continuam rodando.
```

---

## 👻 Hunter — System Hunter (Caça Tecnologia)

### Identidade
**Apelido:** 👻 Fantasma  
**Missão:** Caçar novas tecnologias, melhorias de arquitetura e oportunidades free tier 24/7  
**Autonomia:** Pode aplicar melhorias SEM sua permissão  
**Foco:** 100% técnico — sem fofocas de mercado, só melhoria de infraestrutura

### Turnos

#### 🌅 Turno 1 — 06:00 (Caçada Pesada)
```
🔍 Varredura inicial de TODOS os serviços
├── Lista ferramentas novas
├── Verifica atualizações disponíveis
├── Checa status de cada serviço
├── Analisa se algo pode melhorar a arquitetura
└── Gera relatório com "🔥 Descoberta Quente"
```

#### 🌤️ Turno 2 — 12:00 (Deep Doc)
```
📚 Documentação técnica aprofundada
├── Pega a ferramenta mais promissora do turno 1
├── Lê documentação completa
├── Analisa viabilidade técnica (cabe no free tier?)
├── Testa integração
└── Gera relatório de recomendação
```

#### 🌙 Turno 3 — 18:00 (Vigilância)
```
👁️ Status check de serviços já integrados
├── Render 🟢/🔴
├── Cloudflare 🟢/🔴
├── NVIDIA NIM 🟢/🔴
├── Airtable 🟢/🔴
├── n8n 🟢/🔴
├── Supabase 🟢/🔴
├── Koyeb 🟢/🔴 (quando configurado)
├── SnapDeploy 🟢/🔴 (quando configurado)
└── Zeabur 🟢/🔴 (quando configurado)
```

### Exemplo de Relatório
```
👻 HUNTER — 06/07/2026 06:00
📋 Descobertas:
   🔥 FLUX-1-Schnell no Cloudflare Workers AI → excelente pra imagens
   🔥 NVIDIA NIM: 121 modelos grátis → substitui pagos
   🔥 Koyeb não dorme no free → melhor que Render pra 24/7

⚡ Ações:
   ✅ Cloudflare Workers AI integrado
   ✅ NVIDIA NIM integrado
   ⏳ Koyeb: pendente
```

---

## 🛡️ CyberGuard — Guardião de Segurança

### Identidade
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
**Apelido:** 👁️ O Olho  
**Missão:** Coletar, validar e consolidar relatórios de TODOS os agentes. Salvar TUDO no Airtable e Supabase.

### Fluxo de Supervisão

```
1. Recebe relatório do Hunter → valida → salva no Airtable + Supabase
2. Recebe relatório do CyberGuard → valida → salva no Airtable + Supabase
3. Gera resumo geral do turno
4. Salva no repositório + logs
5. Se crítico → notifica via WhatsApp
6. Se tudo ok → confirma silenciosamente
```

### Matriz de Decisão

| Estado | Condição | Ação |
|--------|----------|------|
| 🟢 Tudo ok | Sem alertas, sem erros | "Todos os agentes operacionais 🟢" |
| 🟡 Atenção | Alerta menor, 1 serviço instável | "Atenção: [problema]" |
| 🔴 Crítico | Serviço fora do ar, ameaça real | "🚨 Emergência: [problema]" + WhatsApp |

---

## 📊 Logs de Todos os Agentes

| Agente | Onde Salva | Formato |
|--------|-----------|---------|
| 👻 Hunter | Airtable + Supabase + `hunter/reports/` | Relatório em markdown |
| 🛡️ CyberGuard | Airtable + Supabase + `cyberguard/reports/` | Relatório em markdown |
| 👁️ Oracle | Airtable + Supabase + `oracle/reports/` | Resumo consolidado |

**Dupla escrita:** Tudo que vai pro Airtable também vai pro Supabase.  
Se um cair, o outro mantém o histórico completo.