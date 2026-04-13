---
projeto: MEMORABILIA
tipo: business-model-pipeline
data: 2026-04-13
versao: v2
status: atual
---

# AI Pipeline Studio — Modelo de Negócio v2

Infraestrutura de Produção Audiovisual com Inteligência Artificial
pingpong · Montreal · April 2026

---

## 1. O Serviço

Pipeline de produção audiovisual com AI, implementado sob medida para studios e agências criativas. Cada implementação é única — calibrada para volume de produção, hardware existente, software em uso e objetivos de crescimento.

O resultado é infraestrutura própria: sem dependência de cloud, sem dados de terceiros, funcionando 24/7 no próprio studio. Custo mensal após setup: zero.

### O que é entregue

- Pipeline de ingest automático — footage entra, estrutura é criada automaticamente
- Transcrição automática Whisper large-v3 (PT, EN, FR + 90 idiomas)
- Geração de proxies 720p para edição fluida
- Indexação semântica ChromaDB — busca por conteúdo em todo o arquivo
- Integração com Premiere Pro e DaVinci Resolve
- Review e aprovação com timecode (Frame.io for Creative Cloud)
- Portal do cliente com status em tempo real (PocketBase self-hosted)
- Entrega de arquivos ao cliente (Nextcloud self-hosted)
- Acesso remoto seguro via WireGuard VPN
- Publicação automática (YouTube, Vimeo) via n8n
- Treinamento da equipe + documentação completa

---

## 2. Client Portal — Stack de Entrega e Aprovação

### O problema

Sem review integrada, o ciclo de aprovação é lento e confuso: cliente comenta em e-mail, editor cruza informações manualmente, versões se perdem em pastas como final_v3_DEFINITIVO. Cada rodada custa tempo e risco de erro.

### O ciclo completo

1. **Discovery** — videochamada (briefing gravado → Whisper transcreve)
2. **Editor finaliza** versão no Premiere / DaVinci
3. **Frame.io** — envia link ao cliente (painel dentro do Premiere/AE)
4. **Cliente** — acessa portal, assiste no browser, comenta com timecode exato, aprova ou solicita ajuste
5. **Editor** — vê comentários dentro do Premiere, corrige, sobe nova versão
6. **PocketBase** — registra aprovação (data + nome + versão)
7. **Nextcloud** — arquivo definitivo entregue com link permanente
8. **n8n** — publicação automática YouTube / Vimeo com notificação

### Stack — 5 camadas integradas

| Camada | Ferramenta | Função | Custo |
|---|---|---|---|
| Review com timecode | Frame.io for Creative Cloud | Comentários dentro do Premiere e AE | Incluído no Adobe CC |
| Portal do cliente | PocketBase (self-hosted) | Status em tempo real · aprovações · histórico | $0 |
| Entrega de arquivos | Nextcloud (self-hosted) | Link de download · arquivo definitivo | $0 |
| Videochamadas | Jitsi Meet (self-hosted) | Discovery · review · entrega final | $0 |
| Automação | n8n (self-hosted) | Notificações · publicação YouTube/Vimeo | $0 |

### PocketBase — o que gerencia por projeto

- Login seguro do cliente (sem senha compartilhada)
- Status em tempo real: "Em edição" → "Aguardando aprovação" → "Aprovado"
- Histórico de versões com data e responsável
- Aprovação registrada formalmente (nome + data)
- Dashboard do studio: todos os projetos em uma tela
- Contratos e briefings por projeto

### Antes vs Depois

| Situação | Sem pipeline | Com pipeline |
|---|---|---|
| Cliente comenta | E-mail · WhatsApp | Frame.io — timecode exato no browser |
| Editor vê feedback | Cruza e-mails | Painel dentro do Premiere |
| Status do projeto | Nenhum | PocketBase — tempo real |
| Versioning | final_v3_DEFINITIVO | Automático por versão |
| Aprovação | Informal | PocketBase — data + nome + versão |
| Arquivo definitivo | Manual · disco local | Nextcloud — link permanente |
| Publicação | Manual · 1-2h | n8n — automático em minutos |

---

## 3. Arquitectura Distribuída

### Pipeline distribuído global

O que transforma um pipeline local em infraestrutura planetária: WireGuard VPN criptografada ponta a ponta conecta todos os nós. RAW footage nunca trafega pela rede — apenas proxies 720p (~400MB/h) e transcrições (~50KB). Dados sensíveis nunca saem da rede privada.

### Nós da rede

| Nó | Localização | Função | Conexão |
|---|---|---|---|
| Hub central | Sede (fixo) | AI · render · storage · portal | — |
| Workstation edição | Sede (fixo) | Premiere/Resolve · render farm · Whisper | LAN |
| Nó remoto | Filial (fixo) | Ingest · Whisper local · proxy | WireGuard |
| Nó móvel | Campo (móvel) | Captação · edição proxy | WireGuard |
| Cliente | Qualquer país | Portal PocketBase · Frame.io · Nextcloud | HTTPS |

### Stack de segurança

- WireGuard VPN — túnel criptografado entre todos os nós
- UFW Firewall — apenas portas necessárias
- SSL/TLS (Nginx Proxy Manager) — HTTPS em todos os serviços
- DuckDNS — DNS dinâmico (IP fixo não necessário)
- Air-gap AI — modelos nunca expostos à internet

### 3 cenários de operação

**Cenário A — Captação remota, processamento central:** Cinegrafista filma em campo → nó remoto faz ingest + proxy + transcrição local → proxy sobe via VPN → hub central processa pipeline completo → editor na sede monta com proxies → render farm finaliza → cliente aprova via portal.

**Cenário B — Colaboração simultânea:** Editor A monta sequência no Resolve (filial) ↔ Editor B faz motion graphics no After Effects (sede) → ambos acessam mesmos proxies via VPN → compositor finaliza → render farm processa → cliente aprova.

**Cenário C — Captação na sede, edição remota:** Footage captado na sede → pipeline processa automaticamente → proxies + análise enviados via VPN ao editor remoto → editor monta com proxy local (sem depender de latência contínua) → decisões voltam ao hub central para depósito de memória.

---

## 4. Três Níveis de Implementação

Valores em CAD. Baseados no mercado canadense 2026.

### Nível 1 — Pequeno Porte

**Perfil:** 2-5 pessoas · 2-4 projetos/mês · sem servidor dedicado

**Inclui:** Recomendação + configuração hardware · estrutura de projetos padronizada · pipeline ingest · Whisper transcrição PT/EN/FR · proxies 720p · integração Premiere · Frame.io (Adobe CC incluso) · PocketBase portal · storage tiers HOT/WARM/COLD · WireGuard VPN · treinamento meio dia · documentação completa.

| Região | Implementação | Retainer mensal | Total Ano 1 |
|---|---|---|---|
| Quebec | $11k-14k | — ou $800-1k/mês | $11k-26k |
| Canada | $13k-17k | — ou $900-1.2k/mês | $13k-31k |
| Global | $15k-20k | — ou $1k-1.5k/mês | $15k-38k |

### Nível 2 — Médio Porte

**Perfil:** 5-15 pessoas · 5-12 projetos/mês · 1 servidor existente ou a instalar

**Inclui tudo do Nível 1 +** Servidor dedicado GPU · ChromaDB indexação semântica · descrição visual por frame · trilha original MusicGen · watchdog ingest automático · tier manager HOT→WARM→COLD · Nextcloud entrega · PocketBase avançado (contratos + faturas) · VPN completa para equipe · FFmpeg exportação multi-plataforma · treinamento dia completo.

| Região | Implementação | Retainer mensal | Total Ano 1 |
|---|---|---|---|
| Quebec | $22k-30k | — ou $1.2k-1.8k/mês | $22k-52k |
| Canada | $26k-36k | — ou $1.4k-2k/mês | $27k-60k |
| Global | $30k-42k | — ou $1.8k-2.5k/mês | $30k-72k |

### Nível 3 — Grande Complexidade

**Perfil:** 15+ pessoas · 12+ projetos/mês · render farm · operação global

**Inclui tudo dos Níveis 1+2 +** Render farm distribuído · ComfyUI geração de imagens/thumbnails · AnimateDiff · pipeline multi-país · dashboard monitoramento tempo real · PocketBase multi-tenant · integração unidades móveis · treinamento 2 dias · SLA contratual.

| Região | Implementação | Retainer mensal | Total Ano 1 |
|---|---|---|---|
| Quebec | $42k-58k | — ou $2k-3k/mês | $42k-94k |
| Canada | $48k-66k | — ou $2.5k-3.5k/mês | $48k-108k |
| Global | $55k-78k | — ou $3k-4.5k/mês | $55k-132k |

---

## 5. Modelos de Receita

### Projeto fixo por entrega
Escopo definido, prazo fixo, pagamento em 3 parcelas (30% início / 40% entrega parcial / 30% entrega final). Ideal para primeiros clientes — valida o produto e gera cases de referência.

### Projeto fixo + Retainer mensal
Implementação como projeto fixo, seguida de contrato mensal: manutenção, updates de modelos AI, suporte prioritário, melhorias incrementais. Modelo recomendado a partir do 2º cliente. Receita previsível + relacionamento longo prazo.

### SaaS on-site mensal
Entrada reduzida seguida de assinatura mensal que cobre toda a infraestrutura como serviço vivo. O switching cost é altíssimo: uma vez integrado ao workflow do studio com PocketBase, Frame.io e n8n, o cliente nunca sai.

---

## 6. ROI para o Cliente

### Economia operacional (2 projetos/mês)

| Ganho | Horas economizadas | Valor estimado/mês |
|---|---|---|
| Transcrição automática Whisper | 3-6h por projeto | $600-1.200 |
| Proxies e estrutura automáticos | 1-2h por projeto | $200-400 |
| Ciclo de review via Frame.io | 2-4h por projeto | $400-800 |
| Busca semântica no arquivo | 2-4h por mês | $200-400 |
| Exportação multi-plataforma | 1-3h por projeto | $200-600 |
| Publicação automática n8n | 1-2h por projeto | $200-400 |
| **Total** | **16-34h/mês** | **$1.800-3.800/mês** |

**Payback:** Nível 1 em 4-8 meses · Nível 2 em 8-14 meses · Nível 3 em 16-24 meses.

### SaaS substituído (economia adicional)

O pipeline substitui um stack equivalente a $2.700-8.000/mês em serviços cloud:

| Serviço substituído | SaaS equivalente | Economia anual |
|---|---|---|
| Review com timecode | Frame.io Pro | $14.400 |
| Portal do cliente | Custom dev ou SaaS | $2.400-6.000 |
| Videoconferência | Zoom/Teams | $2.400-3.600 |
| Transcrição | Rev.com / Sonix | $3.600-18.000 |
| Automação | Zapier / n8n cloud | $2.400-6.000 |
| VPN corporativa | Tailscale Business | $1.200-3.600 |
| Storage cloud | Backblaze B2 | $2.400-9.600 |
| Biblioteca de mídia | Iconik | $6.000-24.000 |
| **Total economizado** | | **$28.800-61.200/ano** |

Custo do pipeline após setup: **$0/mês.**

---

## 7. Diferencial Competitivo

### O que nenhum concorrente oferece

1. **Memória projetual viva** — o pipeline acumula decisões reais entre projetos. O projeto 10 é mais preciso que o projeto 1. Nenhuma ferramenta genérica faz isso.

2. **Privacidade total** — tudo roda em hardware do cliente. Nenhum dado sai da rede. Zero dependência de cloud. Compliance com PIPEDA e regulações de privacidade.

3. **Custo zero de operação** — após setup, o custo mensal é literalmente zero. SaaS equivalente custa $2.700-8.000/mês.

4. **Arquitectura distribuída** — opera de qualquer lugar do mundo via VPN criptografada. Escritório em Toronto, cinegrafista em São Paulo, editor em Montreal — todos no mesmo pipeline.

5. **Indexação semântica** — busca "mulher falando perto do mar" em vez de "clip_047_take3.mov". Nenhum NAS ou DAM tradicional faz busca por significado.

6. **Client portal integrado** — Frame.io + PocketBase + Nextcloud + n8n formam um ciclo completo de entrega e aprovação que substitui 4-5 ferramentas separadas.

---

## 8. Próximo Passo

**Discovery presencial ou remoto — 2 a 3 horas — sem custo.**

Sessão de discovery para mapear workflow atual, hardware disponível e objetivos do studio. Proposta de implementação com escopo, prazo e valor fixos entregue em até 5 dias úteis.

---

*pingpong · Montreal · April 13, 2026 · AI Pipeline Studio · Modelo de Negócio v2*
