# 🏗️ Diagramas de Arquitetura — Atena Ecosystem

> Diagramas em Mermaid — renderizam automaticamente no GitHub.
> Para visualizar, abra qualquer arquivo `.md` no GitHub que contenha blocos ````mermaid`.

---

## 1. 🌐 Arquitetura Geral do Sistema

```mermaid
graph TB
    subgraph "📱 Celular - Tela Burra"
        U[👤 Jessica Gaya]
        WA[📲 WhatsApp]
    end

    subgraph "🧠 Zapia - Cérebro Central"
        Z[🧠 Zapia IA]
        Z --> |Escolhe| Skills
        Z --> |Agenda| Crons
        Z --> |Gerencia| Agentes
        
        subgraph Skills
            S1[📊 Airtable]
            S2[🎨 Cloudflare AI]
            S3[🤖 NVIDIA NIM]
            S4[📝 Copy-Angel]
            S5[🎨 Design-Angel]
            S6[📋 Consórcio]
        end
        
        subgraph Agentes
            A1[👻 Hunter]
            A2[🛡️ CyberGuard]
            A3[👁️ Oracle]
        end
        
        subgraph Crons
            C1[🌅 06:00 Hunter]
            C2[🌤️ 12:00 Hunter]
            C3[🌙 18:00 Hunter]
            C4[🛡️ 06/12/18 CyberGuard]
            C5[📝 23:00 Roteiros]
        end
    end

    subgraph "☁️ Serviços Cloud"
        direction TB
        R[⚙️ Render - n8n]
        CF[🌩️ Cloudflare Workers AI]
        NV[💜 NVIDIA NIM]
        AT[🗄️ Airtable DB]
        GH[🐙 GitHub]
    end

    subgraph "📊 Conteúdo Produzido"
        L[👩‍⚖️ Dra. Luísa]
        LC[👨‍⚖️ Dr. Luciano]
        AS[🎯 Angel Sakura]
    end

    U --> WA --> Z
    Z --> R
    Skills --> AT
    Skills --> CF
    Skills --> NV
    Z --> GH
    Z --> L
    Z --> LC
    Z --> AS
```

---

## 2. 🔄 Fluxo de Agentes e Monitoramento

```mermaid
graph LR
    subgraph "Ciclo de Monitoramento 24/7"
        direction TB
        H[👻 HUNTER<br/>06h/12h/18h] -->|Relatório| O[👁️ ORACLE]
        C[🛡️ CYBERGUARD<br/>06h/12h/18h] -->|Relatório| O
        O -->|Resumo| S[📊 Sistema]
        O -->|Alerta Crítico| WA[📱 WhatsApp]
    end

    subgraph "👻 Hunter - Sub-agentes"
        H1[🔍 Varredura]
        H2[📚 Deep Doc]
        H3[👁️ Vigilância]
    end

    subgraph "🛡️ CyberGuard - Sub-agentes"
        CG1[📡 Port Scanner]
        CG2[🕵️ Threat Monitor]
        CG3[🔐 Firewall Check]
        CG4[🔌 Conexões]
    end

    H1 --> H
    H2 --> H
    H3 --> H
    CG1 --> C
    CG2 --> C
    CG3 --> C
    CG4 --> C
```

---

## 3. 🏛️ Fluxo de Conteúdo (Roteiros)

```mermaid
graph TB
    subgraph "Entrada"
        A[🎤 Áudio da Jessica]
    end

    subgraph "Processamento Zapia"
        Z[🧠 Zapia Interpreta]
        CP[📝 Copy-Angel Skill]
        DA[🎨 Design-Angel Skill]
    end

    subgraph "Produção"
        R3[📋 3 Roteiros<br/>por cliente]
        T[📝 Textos]
        I[🖼️ Imagens]
    end

    subgraph "Entrega"
        W[📲 WhatsApp]
        IG[📸 Instagram]
        TT[🎵 TikTok]
        FB[📘 Facebook]
    end

    subgraph "Clientes"
        L[👩‍⚖️ Dra. Luísa]
        LC[👨‍⚖️ Dr. Luciano]
        AS[🎯 Angel Sakura]
    end

    A --> Z
    Z --> CP
    Z --> DA
    CP --> R3
    R3 --> T
    DA --> I
    T --> W
    T --> IG
    T --> TT
    T --> FB
    IG --> L
    IG --> LC
    IG --> AS
    TT --> AS
    FB --> AS
```

---

## 4. ⚙️ Infraestrutura em Nuvem

```mermaid
graph TB
    subgraph "🌐 Provedores Cloud"
        direction TB
        R1[⚙️ Render<br/>n8n + FreeLLMAPI + Dashboard]
        CF1[🌩️ Cloudflare<br/>Workers AI + R2 Storage]
        NV1[💜 NVIDIA NIM<br/>LLM Inference]
        AT1[🗄️ Airtable<br/>Banco de Dados]
        GH1[🐙 GitHub<br/>Código + Portfólio]
    end

    subgraph "Estratégia de Balanceamento"
        B1[1️⃣ Render ✅]
        B2[2️⃣ Koyeb]
        B3[3️⃣ Zeabur]
        B4[4️⃣ SnapDeploy]
        B5[5️⃣ PC Local]
    end

    R1 --- B1
    B1 --> B2 --> B3 --> B4 --> B5

    CF1 --> R1
    NV1 --> R1
    AT1 --> R1
    GH1 --> R1
```

---

## 5. 🗓️ Grade de Conteúdo Diária

```mermaid
gantt
    title Grade de Conteúdo - Dra. Luísa
    dateFormat HH:mm
    axisFormat %H:%M
    
    section Stories
    Story Matinal      :s1, 08:00, 1h
    Story 12h          :s2, 12:00, 1h
    Story 18h          :s3, 18:00, 1h
    
    section Reels
    Reel 15h           :r1, 15:00, 1h
    Reel 20:30         :r2, 20:30, 1h
```

```mermaid
gantt
    title Produção de Roteiros (Zapia)
    dateFormat HH:mm
    axisFormat %H:%M
    
    section Geração
    Roteiros Luísa     :g1, 23:00, 2h
    Roteiros Luciano   :g2, 08:00, 2h
    Roteiros Angel S.  :g3, 09:00, 2h
```