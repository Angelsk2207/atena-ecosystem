# ⚙️ Infraestrutura Técnica

## Visão Geral

O ecossistema Atena roda 100% em serviços gratuitos, distribuídos em múltiplos provedores para garantir redundância.

---

## 🗺️ Mapa de Infraestrutura

```
                    ┌──────────────────────────────────┐
                    │       GitHub (Código)             │
                    │  ├── Repositórios públicos        │
                    │  ├── GitHub Pages (portfólio)     │
                    │  └── Deploy automático            │
                    └──────────┬───────────────────────┘
                               │
           ┌───────────────────┼───────────────────────┐
           ▼                   ▼                       ▼
    ┌────────────┐    ┌──────────────┐    ┌──────────────────┐
    │  Render    │    │ Cloudflare   │    │   Airtable        │
    │  (n8n)     │    │ Workers AI   │    │   (Banco de Dados)│
    │  FreeLLMAPI │    │ R2 Storage   │    │                  │
    │  Dashboard │    │              │    │ Clientes, Rots   │
    └────────────┘    └──────────────┘    └──────────────────┘
```

---

## 📦 Serviços Detalhados

### 1. Render (Free Tier)

| Serviço | URL | Status |
|---------|-----|--------|
| n8n | https://atena-n8n.onrender.com | 🟢 |
| FreeLLMAPI | https://freellmapi-atena.onrender.com | 🟢 |
| Dashboard Atena | https://dashboard-atena.onrender.com | 🟢 |

**Características:**
- Free tier: 512MB RAM, 1 CPU
- Dorme após 15 min de inatividade
- Acorda em ~30 segundos

### 2. Cloudflare Workers (Free Tier)

| Serviço | Função | Limite |
|---------|--------|--------|
| Workers AI | Geração de imagens (FLUX, SDXL) | 10k neurônios/dia |
| R2 Storage | Armazenamento de arquivos | 10GB grátis |
| Workers | Funções serverless | 100k requisições/dia |

### 3. Airtable (Free Tier)

| Base | Função |
|------|--------|
| Dashboard Atena | CRUD de clientes, roteiros, cache de skills |

**Características:**
- 1.000 registros por base
- API RESTful com PAT
- Interface visual para edição manual

### 4. NVIDIA NIM (Free Tier)

| Serviço | Função | Limite |
|---------|--------|--------|
| LLM Inference | Mistral, Qwen, Llama, DeepSeek | 40 RPM, 121+ modelos |

### 5. GitHub (Free Tier)

| Repositório | Função |
|-------------|--------|
| atena-os | Sistema de agentes e monitoramento |
| atena-n8n | Orquestrador N8N |
| freellmapi-atena | Proxy OpenAI-compatible |
| atena-video-editor | Editor de vídeo open source |
| + diversos | Portfólio, sites, experimentos |

---

## 🔐 Credenciais e Acesso

| Serviço | Credencial | Status |
|---------|------------|--------|
| Airtable | PAT (Personal Access Token) | ✅ Configurado |
| Cloudflare | API Token | ✅ Configurado |
| NVIDIA NIM | API Key | ✅ Configurado |
| GitHub | Token (PAT clássico) | ✅ Configurado |
| Render | API Key | ✅ Configurado |
| Supabase | Anon Key | ⏳ Aguardando login |

---

## 📊 Performance e Limites

### Free Tier Limits

| Serviço | Limite Principal | Consumo Atual |
|---------|-----------------|---------------|
| Zapia | 500 mensagens/mês | Baixo |
| Airtable | 1.000 registros/base | ~100 registros |
| Cloudflare AI | 10k neurônios/dia | ~50 neurônios/dia |
| NVIDIA NIM | 40 RPM | ~5 RPM |
| Render | 512MB RAM | ~200MB |
| Kaggle | 30h GPU/semana | 0h (não usado) |

### Otimizações Aplicadas

- **Regra Nano 🪶** — Todo deploy usa versão mínima (Alpine, sem frontend)
- **Cache** — Resultados frequentes são cacheados no Airtable
- **Compressão** — Tráfego entre serviços é comprimido
- **Sleep/Wake** — Serviços que dormem economizam recursos

---

## 📈 Plano de Expansão

### Próximos Passos (Prioridade)

```
1. ✅ Zapia + Skills funcionando
2. ✅ Agentes de monitoramento (Hunter, CyberGuard, Oracle)
3. ✅ Pipeline de roteiros (clientes)
4. ⏳ Postagem automática em redes sociais
5. ⏳ Dashboard de analytics
6. ⏳ Captura de leads automatizada
7. ⏳ Dupla escrita Airtable + Supabase
```

### Migrações Futuras

| Serviço Atual | Migrar Para | Quando |
|--------------|-------------|--------|
| Airtable | Supabase (ou manter ambos) | Após login |
| Render (n8n) | SnapDeploy/Koyeb | Quando precisar |
| Zapia gratuito | Zapia Pro | Se precisar de mais crons |