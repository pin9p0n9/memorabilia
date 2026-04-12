---
projeto: MEMORABILIA
tipo: business-model-pipeline
data: 2026-04-12
tags:
  - pipeline
  - serviço
  - business
  - studios
status: atual
---

# AI Pipeline Studio — Modelo de Negócio

Infraestrutura de Produção Audiovisual com Inteligência Artificial
pingpong · Montreal · April 2026

---

## 1. O Serviço

Pipeline de produção audiovisual com AI, implementado sob medida para studios e agências criativas. Cada implementação é única — calibrada para volume de produção, hardware existente, software em uso e objetivos de crescimento.

O resultado é infraestrutura própria: sem dependência de cloud, sem dados de terceiros, funcionando 24/7 no próprio studio. Custo mensal após setup: zero.

### O que é entregue

- Pipeline de ingest automático — footage entra, estrutura é criada
- Transcrição automática Whisper large-v3 (PT, EN, FR + 90 idiomas)
- Geração de proxies 720p para edição fluida
- Indexação semântica ChromaDB — busca por conteúdo em todo o arquivo
- Integração Premiere Pro e DaVinci Resolve
- Review e aprovação com timecode (Frame.io for Creative Cloud)
- Portal do cliente com status em tempo real (PocketBase self-hosted)
- Acesso remoto seguro via VPN
- Publicação automática (YouTube, Vimeo) via n8n
- Treinamento da equipe + documentação completa

---

## 2. Client Portal — Stack de Entrega e Aprovação

### O problema

Sem review integrada, o ciclo de aprovação é lento: cliente comenta em e-mail, editor cruza manualmente, versões se perdem em pastas como final_v3_DEFINITIVO. Cada rodada custa tempo e risco.

### Como funciona

Editor finaliza → envia link Frame.io → cliente assiste no browser sem instalar nada → comenta com timecode exato → editor vê comentários dentro do Premiere → corrige → sobe nova versão → ciclo até aprovação → PocketBase registra → Nextcloud entrega arquivo definitivo → n8n publica automaticamente.

### Stack do portal — 4 camadas integradas

| Camada | Ferramenta | Função | Custo |
|---|---|---|---|
| Review | Frame.io for CC | Comentários dentro do Premiere/AE | Incluso Adobe CC |
| Portal | PocketBase | Status tempo real · aprovações · histórico | $0 |
| Entrega | Nextcloud | Link download · arquivo definitivo | $0 |
| Automação | n8n | Notificações · publicação YouTube/Vimeo | $0 |

### Antes vs Depois

| Situação | Sem pipeline | Com pipeline |
|---|---|---|
| Cliente comenta | E-mail · WhatsApp | Frame.io — timecode exato |
| Editor vê feedback | Cruza e-mails | Painel dentro do Premiere |
| Status do projeto | Nenhum | PocketBase — tempo real |
| Versioning | final_v3_DEFINITIVO | Automático |
| Aprovação | Informal | PocketBase — data + nome |
| Publicação | Manual · 1-2h | n8n — automático |

---

## 3. Arquitectura Distribuída

Pipeline distribuído global via VPN criptografada:

- **Hub central** — servidor AI com GPU, transcrição, indexação, orquestração
- **Workstation edição** — Premiere/Resolve, render farm, Whisper local
- **Nó remoto** — ingest em campo, proxy local, transcrição
- **Nó móvel** — captação, edição proxy, monitoramento
- **Cliente** — portal PocketBase, Frame.io, Nextcloud — qualquer browser, qualquer país

### Fluxo distribuído

Captação em qualquer lugar → VPN criptografada → hub central processa (transcrição + indexação + análise) → editor trabalha com proxies → render farm finaliza → Frame.io para review → PocketBase registra aprovação → n8n publica.

Dados sensíveis nunca saem da rede privada. RAW footage nunca trafega — apenas proxies e transcrições.

---

## 4. Três Níveis de Implementação

Valores em CAD. Baseados no mercado canadense 2026.

### Nível 1 — Pequeno Porte

**Perfil:** 2-5 pessoas · 2-4 projetos/mês

**Inclui:** Hardware recomendação, estrutura de projetos, pipeline ingest, Whisper, proxies, Premiere integration, Frame.io, PocketBase, storage tiers, VPN, treinamento meio dia.

| Modelo | Implementação | Recorrente | Total Ano 1 |
|---|---|---|---|
| Projeto fixo | $11k-14k | — | $11k-14k |
| Fixo + Retainer | $11k-14k | $800-1k/mês | $21k-26k |
| SaaS mensal | $2.5k-4k | $1.8k-2.5k/mês | $24k-34k |

### Nível 2 — Médio Porte

**Perfil:** 5-15 pessoas · 5-12 projetos/mês

**Inclui:** Tudo do Nível 1 + servidor dedicado GPU, ChromaDB, descrição visual por frame, MusicGen, watchdog automático, tier manager, Nextcloud, PocketBase avançado, VPN completa, treinamento dia completo.

| Modelo | Implementação | Recorrente | Total Ano 1 |
|---|---|---|---|
| Projeto fixo | $22k-30k | — | $22k-30k |
| Fixo + Retainer | $22k-30k | $1.2k-1.8k/mês | $36k-52k |
| SaaS mensal | $5k-8k | $3k-4.5k/mês | $41k-62k |

### Nível 3 — Grande Complexidade

**Perfil:** 15+ pessoas · 12+ projetos/mês · render farm · operação global

**Inclui:** Tudo dos Níveis 1+2 + render farm distribuído, publicação automática, ComfyUI, pipeline multi-país, dashboard monitoramento, PocketBase multi-tenant, integração móvel, treinamento 2 dias, SLA.

| Modelo | Implementação | Recorrente | Total Ano 1 |
|---|---|---|---|
| Projeto fixo | $42k-58k | — | $42k-58k |
| Fixo + Retainer | $42k-58k | $2k-3k/mês | $66k-94k |
| SaaS mensal | $8k-14k | $5.5k-8k/mês | $74k-110k |

---

## 5. Modelos de Receita

**Projeto fixo:** Escopo definido, pagamento 30/40/30. Ideal para primeiros clientes — valida e gera cases.

**Fixo + Retainer:** Implementação + manutenção mensal com updates AI, suporte prioritário, melhorias. Receita previsível. Recomendado a partir do 2º cliente.

**SaaS on-site:** Entrada reduzida + assinatura mensal. Switching cost altíssimo — uma vez integrado com PocketBase, Frame.io e n8n, o cliente nunca sai.

---

## 6. ROI para o Cliente

| Ganho | Economia/mês |
|---|---|
| Transcrição automática | $600-1.200 |
| Proxies + estrutura | $200-400 |
| Ciclo review Frame.io | $400-800 |
| Busca semântica | $200-400 |
| Exportação + publicação | $400-1.000 |
| **Total (2 proj/mês)** | **$1.800-3.800** |

**Payback:** Nível 1 em 4-8 meses · Nível 2 em 8-14 meses · Nível 3 em 16-24 meses.

### SaaS substituído

O pipeline substitui um stack equivalente a $2.700-8.000/mês em serviços cloud:

| Serviço | SaaS equivalente | Economia/ano |
|---|---|---|
| Review com timecode | Frame.io Pro | $14.400 |
| Portal do cliente | Custom/SaaS | $2.400-6.000 |
| Transcrição | Rev.com / Sonix | $3.600-18.000 |
| Automação | Zapier / n8n cloud | $2.400-6.000 |
| VPN corporativa | Tailscale Business | $1.200-3.600 |
| Storage cloud | Backblaze B2 | $2.400-9.600 |
| **Total economizado** | | **$28.800-61.200/ano** |

Custo do pipeline após setup: **$0/mês.**

---

*pingpong · Montreal · April 2026 · AI Pipeline Studio · Modelo de Negócio*
