# 🧩 Componentes do Ecossistema Atena

## 1. 🧠 Zapia — Cérebro Central

O Zapia é o orquestrador de todo o ecossistema. Ele:

- **Interpreta** comandos de voz/áudio da Jessica
- **Escolhe** a skill certa para cada tarefa
- **Executa** automações programadas (crons)
- **Gerencia** agentes (Hunter, CyberGuard, Oracle)
- **Entrega** resultados via WhatsApp

### Skills Instaladas

| Skill | Tipo | Função |
|-------|------|--------|
| **airtable** | 🧩 Dados | CRUD de clientes, roteiros, cache |
| **cloudflare-ai** | 🎨 Imagem | Geração via FLUX, SDXL, Dreamshaper |
| **nvidia-nim** | 🤖 LLM | Texto via Mistral, Qwen, Llama |
| **copy-angel** | ✍️ Copy | Roteiros, scripts, CTAs, legendas |
| **design-angel** | 🎨 Design | Pesquisa Pinterest + geração visual |
| **hunter-angelos** | 👻 Scout | Caça de tecnologias 24/7 |
| **consorcio-copywriter** | 📋 Copy | Copywriting para consórcio |
| **agent-vendedor-angel** | 💼 Vendas | Prospecção por e-mail |
| **inkscape-vector** | 🖌️ Design | Edição vetorial profissional |
| **penpot-design** | 🎨 UI/UX | Design de interfaces (Figma-like) |
| **polotno-studio** | 🖼️ Design | Editor tipo Canva |
| **video-ai-scout** | 🎬 Pesquisa | Recomendação de apps de vídeo |

---

## 2. 👻 Hunter — Caçador de Tecnologias

**Propósito:** 24/7 varrendo o ecossistema em busca de novas ferramentas, atualizações e melhorias.

### Turnos

| Turno | Horário | Foco |
|-------|---------|------|
| 🌅 Turno 1 | 06:00 | **Caçada Pesada** — Varredura completa de novas ferramentas |
| 🌤️ Turno 2 | 12:00 | **Deep Doc** — Documentação técnica de ferramentas promissoras |
| 🌙 Turno 3 | 18:00 | **Vigilância** — Status dos serviços já integrados |

### O que ele monitora

- **SnapDeploy** — Status do free tier
- **NVIDIA NIM** — RPM e disponibilidade
- **Postiz** — Atividade do repositório
- **n8n** — Community Edition
- **Supabase** — Free tier
- **Cloudflare** — Workers/R2
- **Kaggle** — GPU horas/semana
- **Render** — Status do n8n e FreeLLMAPI

### Autonomia
Hunter tem permissão para **aplicar melhorias automaticamente** — atualizações de pacotes, otimizações de performance, migrações. Só pergunta se for mudar o fluxo de trabalho do usuário.

---

## 3. 🛡️ CyberGuard — Segurança

**Propósito:** Monitoramento de segurança 24/7, 3 turnos/dia.

### Sub-agentes

| Sub-agente | Função |
|------------|--------|
| 📡 Port Scanner | Verifica portas abertas no sistema |
| 🕵️ Threat Monitor | Detecta processos suspeitos |
| 🔐 Firewall Check | Analisa configurações de rede |
| 🔌 Conexões Ativas | Monitora conexões estabelecidas |

---

## 4. 👁️ Oracle — Supervisor

**Propósito:** Coletar relatórios dos agentes, validar, gerar resumo consolidado.

### Fluxo
```
Hunter → relatório → Oracle
CyberGuard → relatório → Oracle
Oracle → consolida → salva → notifica se urgente
```

---

## 5. 🎨 Design Angel — Criação Visual

### Fluxo de Criação
```
1. Prompt do usuário → Zapia
2. Zapia → Design Angel (skill)
3. Design Angel → Pinterest (busca referências)
4. Design Angel → Mostra ao usuário (aprovação)
5. Usuário ajusta → Design Angel → Cloudflare AI (gera imagem)
6. Entrega via WhatsApp
```

### Modelos de IA
- **FLUX-1-Schnell** → Rápido, padrão
- **FLUX-2-Dev** → Premium, mais qualidade
- **SDXL** → Alta qualidade
- **Dreamshaper-8-LCM** → Rápido

---

## 6. 📱 Pipeline de Conteúdo

### Clientes Ativos

| Cliente | Área | Formato | Frequência |
|---------|------|---------|------------|
| **Dra. Luísa** | Direito Criminal | 3 roteiros/dia (story + reel) | Diário 23h |
| **Dr. Luciano** | Direito Civil | 3 roteiros/dia | Semanal Sáb 8h |
| **Angel Sakura** | Agência Design+Tech | 3 roteiros/dia + dicas | Semanal Sáb 9h |

### Estrutura do Roteiro
```
Story Manhã (9h) → Story 12h chamando Reel 15h → Story 18h chamando Reel 20:30
```

### Formatos que Funcionam ✅
- Tutorial com tela gravada
- Comparação prática (antes/depois)
- Processo criativo (briefing → resultado)
- Erro aprendido / como consertar

### Formatos que NÃO Funcionam ❌
- Respondendo perguntas (perfil pequeno)
- Slide com texto
- Apresentação pessoal / câmera na cara
- Lives
- Vídeo com rosto

---

## 7. ⚙️ Infraestrutura

### Serviços Ativos

| Serviço | Onde | Plano | Status |
|---------|------|-------|--------|
| n8n | Render | Free | 🔴 (projeto antigo) |
| FreeLLMAPI | Render | Free | 🟢 |
| Dashboard Atena | Render | Free | 🟢 |
| Cloudflare Workers | Cloudflare | Free | 🟢 |
| Cloudflare R2 | Cloudflare | Free (10GB) | 🟢 |
| Airtable | Airtable | Free | 🟢 |
| GitHub | GitHub | Free | 🟢 |

### Estratégia de Balanceamento (4 nuvens + 1 local)

```
1️⃣ Render ✅ → 2️⃣ Koyeb ➡️ → 3️⃣ Zeabur ➡️ → 4️⃣ SnapDeploy ➡️ → 5️⃣ PC Local
                                                      
Se uma cair, a próxima assume. Zero downtime.
```