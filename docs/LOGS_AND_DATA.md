# 🗄️ Logs e Dados — Dupla Escrita

## A Filosofia: "Nunca Perder Nada"

> Tudo que acontece no ecossistema é registrado em **DOIS lugares** ao mesmo tempo.
> Se Airtable cair → Supabase mantém. Se Supabase cair → Airtable mantém.
> Zero perda de dados.

---

## 🗺️ Fluxo de Dados

```
🧠 Zapia executa ação
    │
    ├── Salva no 📊 AIRTABLE (banco principal)
    │      └── Clientes, roteiros, relatórios, cache
    │
    └── Duplica no 🗄️ SUPABASE (banco secundário)
           └── Backup completo de tudo
```

---

## 📊 Airtable — Banco Principal 🟢

**Status:** ✅ Funcionando  
**Base ID:** `apppevGG558uHLYVB`  
**API Key:** Configurada via skill

### O que armazena:

| Tabela | Conteúdo | Exemplo |
|--------|----------|---------|
| 📋 **Clientes** | Dados de cada cliente | Dra. Luísa, Dr. Luciano, Angel Sakura |
| 📝 **Roteiros** | Conteúdo gerado por dia | "3 roteiros Luísa 24/07" |
| 📊 **Relatórios** | Logs dos agentes | "Hunter 06h: tudo ok 🟢" |
| 🗃️ **Cache** | Dados temporários | Resultados de buscas recentes |

---

## 🗄️ Supabase — Banco Secundário 🔄

**Status:** 🔄 Em implementação (aguardando login)  
**Host:** `nkklmerggiwmevlmfjnb.supabase.co`  
**Anon Key:** Configurada

### O que vai armazenar:

| Tabela | Conteúdo | Relação com Airtable |
|--------|----------|---------------------|
| 📋 **clientes** | Mesmos dados do Airtable | Backup |
| 📝 **roteiros** | Mesmos dados do Airtable | Backup |
| 📊 **logs_agentes** | Relatórios dos agentes | Backup |
| 📈 **metricas** | Métricas de desempenho | Exclusivo Supabase |

### Por que Supabase além do Airtable?
- **PostgreSQL** real — consultas complexas possíveis
- **Realtime** — dá pra fazer dashboards ao vivo
- **Backup automático** — se Airtable tiver limite, Supabase segura
- **Custo:** R$ 0 (free tier com 500MB)

---

## 🔄 Estratégia de Dupla Escrita

```
Ação → Escreve no Airtable → Confirmação → Escreve no Supabase
                                              │
                                              ▼
                                      Se falhar → Log de erro → Tenta de novo depois
```

### Se Airtable cair:
1. Zapia detecta falha na escrita
2. Escreve só no Supabase
3. Oracle registra: "Airtable offline"
4. Quando Airtable voltar, sincroniza dados perdidos

### Se Supabase cair:
1. Zapia detecta falha na escrita
2. Continua só no Airtable (normal)
3. Oracle registra: "Supabase offline"
4. Quando Supabase voltar, sincroniza dados perdidos

---

## 🐙 GitHub — Código e Documentação

**Status:** ✅ Público  
**User:** `Angelsk2207`  
**Token:** Configurado

### Repositórios do Ecossistema:

| Repositório | Descrição | Link |
|-------------|-----------|------|
| **atena-ecosystem** | 🌌 Este projeto — arquitetura completa | [GitHub](https://github.com/Angelsk2207/atena-ecosystem) |
| **atena-n8n** | ⚙️ n8n workflow no Render | [GitHub](https://github.com/Angelsk2207/atena-n8n) |
| **freellmapi-atena** | 🧠 FreeLLMAPI proxy | [GitHub](https://github.com/Angelsk2207/freellmapi-atena) |
| **AngelOS** | 🖥️ Sistema operacional adaptativo com IA | [GitHub](https://github.com/Angelsk2207/AngelOS) |
| **AngelOS-2.0** | ☁️ Nuvem própria para PCs antigos | [GitHub](https://github.com/Angelsk2207/AngelOS-2.0) |
| **AngelOS-Aws-local** | 🏗️ Arquitetura AWS local | [GitHub](https://github.com/Angelsk2207/AngelOS-Aws-local) |
| **atena-os** | 🌌 Sistema de agentes original | [GitHub](https://github.com/Angelsk2207/atena-os) |
| **atena-video-editor** | 🎬 Editor de vídeo open source | [GitHub](https://github.com/Angelsk2207/atena-video-editor) |
| **angelsakura.github.io** | 🎯 Site da Angel Sakura | [GitHub](https://github.com/Angelsk2207/angelsakura.github.io) |
| **Angelsk2207.github.io** | 👤 Portfólio pessoal | [GitHub](https://github.com/Angelsk2207/Angelsk2207.github.io) |

---

## 📊 Resumo de Armazenamento

| Onde | O que guarda | Status | Limite Free |
|------|-------------|--------|-------------|
| 📊 Airtable | Dados ativos (clientes, roteiros, logs) | 🟢 | 1.000 registros/base |
| 🗄️ Supabase | Backup completo + métricas | 🔄 | 500MB + 2GB banda |
| 🐙 GitHub | Código + documentação | 🟢 | Ilimitado (público) |
| ☁️ Cloudflare R2 | Arquivos e mídia | 🟢 | 10GB |
| 🗃️ Workspace Zapia | Cache temporário | 🟢 | 100MB |