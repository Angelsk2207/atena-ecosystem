# ☁️ As 5 Nuvens do Ecossistema Atena

> O coração do **Peso Zero**. Tudo que travava ou dava bug no POCO C85 foi migrado para 5 nuvens gratuitas.
> O celular não processa mais nada — só transmite.

---

## 🗺️ Mapa das 5 Nuvens

```
                    ┌──────────────────────────────────────┐
                    │          POCO C85 (Tela Burra)        │
                    │  Só transmite: WhatsApp + Termux      │
                    └──────────────┬───────────────────────┘
                                   │
         ┌─────────────────────────┼─────────────────────────┐
         │                         │                         │
         ▼                         ▼                         ▼
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│  ☁️ RENDER  🟢   │  │ ☁️ CLOUDFLARE 🟢 │  │   ☁️ KOYEB  ⏳   │
│                  │  │                  │  │                  │
│ 🟢 n8n           │  │ 🟢 Workers AI    │  │ Backup n8n       │
│ 🟢 FreeLLMAPI    │  │ 🟢 R2 10GB       │  │ Backup FreeLLMAPI│
│ 🟢 Dashboard     │  │ 🟢 Tunnel        │  │                  │
└──────────────────┘  └──────────────────┘  └──────────────────┘
         │                         │
         ▼                         ▼
┌──────────────────┐  ┌──────────────────┐
│ ☁️ SNAPDEPLOY⏳  │  │  ☁️ ZEABUR  ⏳   │
│                  │  │                  │
│ Deploys rápidos  │  │ Redundância extra│
│ Testes           │  │ Fallback final   │
└──────────────────┘  └──────────────────┘
```

---

## 1️⃣ ☁️ RENDER — Nuvem Principal 🟢

**Status:** ✅ Já funcionando  
**Plano:** Free (dorme após inatividade)  
**Custo:** R$ 0

### O que roda:

| Serviço | URL | O que faz |
|---------|-----|-----------|
| ⚙️ **n8n** | https://atena-n8n.onrender.com | Orquestrador de workflows e agentes |
| 🧠 **FreeLLMAPI** | https://freellmapi-atena.onrender.com | Proxy de 69 modelos de IA (OpenAI-compatible) |
| 📊 **Dashboard Atena** | `dashboard-atena/` | Painel de controle visual |

### Por que Render?
- Primeira nuvem configurada
- Conectada direto ao GitHub (deploy automático)
- Suporte a Docker
- Ideal pra serviços que podem dormir (n8n, dashboard)

---

## 2️⃣ ☁️ CLOUDFLARE — Nuvem de IA e Armazenamento 🟢

**Status:** ✅ Já funcionando  
**Plano:** Free  
**Custo:** R$ 0

### O que roda:

| Serviço | O que faz | Limite |
|---------|-----------|--------|
| 🎨 **Workers AI** | Geração de imagens (FLUX-1-Schnell, SDXL, Dreamshaper) | 10k neurônios/dia |
| 🗂️ **R2 Storage** | Armazenamento de arquivos e mídia | 10GB grátis |
| 🔒 **Tunnel** | Conexão segura sem expor IP | Ilimitado |

### Modelos de IA disponíveis:
- `@cf/black-forest-labs/flux-1-schnell` — Rápido
- `@cf/black-forest-labs/flux-2-dev` — Premium
- `@cf/stabilityai/stable-diffusion-xl-base-1.0` — Alta qualidade

### Por que Cloudflare?
- Melhor infraestrutura de edge computing gratuita
- Geração de imagem sem precisar de GPU local
- R2 substitui S3 da Amazon de graça
- Tunnel elimina necessidade de IP fixo

---

## 3️⃣ ☁️ KOYEB — Nuvem de Backup ⏳

**Status:** 🔄 Pendente  
**Plano:** Free (NÃO dorme — vantagem sobre Render)  
**Custo:** R$ 0

### O que vai rodar:
- Backup do n8n (caso Render durma)
- Backup do FreeLLMAPI
- Mesmo Dockerfile do Render, deploy espelhado

### Por que Koyeb?
- **Não dorme** no free tier (Render dorme)
- Mesma facilidade de deploy via GitHub
- Ideal pra manter serviços críticos 24/7

---

## 4️⃣ ☁️ SNAPDEPLOY — Nuvem de Deploy Rápido ⏳

**Status:** 🔄 Pendente (conta já criada)  
**Plano:** Free (10 deploys/dia)  
**Custo:** R$ 0  
**Login:** gayaskmkt@gmail.com

### O que vai rodar:
- Testes de novos serviços
- Protótipos rápidos
- Versões experimentais antes de ir pro Render

### Por que SnapDeploy?
- Deploy em segundos
- Ótimo pra testar antes de subir em produção
- 10 deploys/dia no free tier

---

## 5️⃣ ☁️ ZEABUR — Nuvem de Redundância Extra ⏳

**Status:** 🔄 Pendente  
**Plano:** Free (1 servidor gerenciável)  
**Custo:** R$ 0

### O que vai rodar:
- Última camada de fallback
- Se todas as outras 4 nuvens caírem (improvável), Zeabur segura

### Por que Zeabur?
- Mais um provedor free pra redundância
- Fácil integração com GitHub
- Camada extra de segurança

---

## 🔄 Estratégia de Balanceamento

```
1️⃣ Render (principal)     → Se cair → 2️⃣ Koyeb assume
2️⃣ Koyeb (backup)         → Se cair → 3️⃣ SnapDeploy assume
3️⃣ SnapDeploy (testes)    → Se cair → 4️⃣ Zeabur assume
4️⃣ Zeabur (redundância)   → Fallback final
5️⃣ POCO C85 (só transmite)→ Nada roda aqui, não importa se cair
```

**Dados ficam no Airtable + Supabase (dupla escrita), nunca nas nuvens.**  
Se uma nuvem cair, os dados não são perdidos.

---

## 📊 Resumo

| # | Nuvem | Status | Função Principal | Dorme? |
|---|-------|--------|-----------------|--------|
| 1 | Render | 🟢 | n8n + FreeLLMAPI + Dashboard | Sim |
| 2 | Cloudflare | 🟢 | Workers AI + R2 + Tunnel | Não |
| 3 | Koyeb | ⏳ | Backup n8n + FreeLLMAPI | Não |
| 4 | SnapDeploy | ⏳ | Deploys rápidos e testes | Não |
| 5 | Zeabur | ⏳ | Redundância extra | Não |

**Próximo passo:** Configurar Koyeb, SnapDeploy e Zeabur com os mesmos serviços do Render.