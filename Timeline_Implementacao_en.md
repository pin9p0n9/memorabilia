---
projeto: MEMORABILIA
tipo: timeline
data: 2026-04-12
tags:
  - timeline
  - implementação
  - homelab
  - histórico
status: atual
---

# MEMORABILIA — Timeline de Implementação

Do zero ao pipeline audiovisual com memória viva.
pingpong · Montreal · Janeiro–Abril 2026

---

## Janeiro 2026 — Primeiras notas

**28 Jan** — Primeira nota no Joplin: "Some mistakes take you to the right place." Início do registro digital.

**01 Feb** — Graphic Design: The New Basics. Primeiras referências de design indexadas.

**07–09 Feb** — Motion Brand Design System · Brand Design with Grids · Layout Design · MASTER AI · Motion Design MASTER. Fundação teórica do repertório visual.

---

## Março 2026 — Week 1: Linux from zero

**09 Mar** — Ubuntu 24.04 LTS installed no HomeLab (ASUS X99-A II · i7-6800K · 2× GTX 1080 Ti · 128GB RAM). Dia zero da infraestrutura.

**09–14 Mar** — 12 lições Linux completadas: terminal, arquivos, permissões, processos, pacotes, redes, .bashrc, scripts, cron, SSH. Driver NVIDIA 580 installed. Wi-Fi RTL8812AU configurado. HD DATA 1.8TB formatado ext4.

**14 Mar** — Primeiro documento de referência: `homelab_guia_LINUX_10`. Joplin installed como sistema de notas.

---

## Março 2026 — Week 2: Cloud + VPN + AI

**15 Mar** — Docker + Nextcloud deployed. MariaDB + Redis. Dados no DATA 1.8TB.

**15 Mar** — Jellyfin deployed (:8096). 292GB mídia transferida do BLACKBOX. 4 dispositivos: Linux, Windows, Roku, Android.

**15 Mar** — WireGuard VPN operacional. HomeLab (10.0.0.1) · Windows (10.0.0.2) · Samsung (10.0.0.3). Split tunneling mobile.

**15 Mar** — Nginx Proxy Manager + DuckDNS + Let's Encrypt SSL wildcard. HTTPS Nextcloud + Jellyfin.

**15 Mar** — Segurança: SSH key-only ED25519 · GPG backups · KeePassXC · Joplin E2E · 2FA Nextcloud · UFW firewall.

**15 Mar** — Ollama installed. Dual GPU tensor split (22GB VRAM). qwen2.5:32b @ 8.82 t/s. Open WebUI com HTTPS.

**15 Mar** — Persona "Jeremias" criada no Open WebUI. AI 100% offline (OLLAMA_NO_CLOUD=true).

**17 Mar** — Phases 1 (Linux), 2 (Nextcloud), 2.5 (Jellyfin+VPN), 2.6 (HTTPS+Security), 3 (AI) — todas COMPLETAS. Python venv configurado.

---

## Março 2026 — Week 3: Arquitetura + Pipeline design

**18 Mar** — Pipeline híbrido desenhado: Luma Labs + HomeLab. Creative AI Learning Path documentado.

**19 Mar** — Roadmap de implementação. Análise honesta: "hardware profissional, pipeline 90% documentado, 10% implementado."

**21 Mar** — Pipeline Audiovisual especificado (Brazil 1970/1982 como analogia). K3s avaliado e descartado — Docker Compose suficiente por agora. Hardware inventory completo (3 machines + Mac Mini futuro).

**22 Mar** — Knowledge Pipeline desenhado: RAG + QLoRA. Visual Library Pipeline especificado. Interface RAG desenhada.

**23 Mar** — Master Summary: 3 peers VPN ativos, benchmarks documentados, modelos pingpong-* criados (full, motion, pm, 3d, mid, quick).

**24 Mar** — GPU stabilization. Plano de manutenção HomeLab. Runbook SRE criado.

**25 Mar** — Roadmap completo atualizado. BLACKBOX formatado NTFS. Decision: Docker Compose por agora, K3s quando 3+ nodes.

---

## Março 2026 — Week 4: Pipeline v1 + SMB + Windows

**27 Mar** — Windows PC hardening completo: BIOS atualizado, drivers verificados, Power Plan High Performance, startup limpo. Checklist de implementação criado.

**27 Mar** — SMB share configurado bidirecional. HomeLab ↔ Windows via Samba + CIFS. DaVinci Resolve conectado ao HomeLab.

**27 Mar** — D:\TOOLS\ criado. project_launcher.py (GUI), pipeline_v1.py (5 etapas), new_project.ps1. Primeiro projeto testado: 260328_V_MAGELLA.

**28 Mar** — Pipeline v1 completo: FFmpeg extrai áudio → Whisper large-v3 transcreve → proxy 720p NVENC → CSV Premiere. Cache inteligente, detecção automática de idioma, fallback CPU.

---

## Março 2026 — Week 5: RAG Pipeline

**29 Mar** — ChromaDB deployed (:8000). LLaVA frame indexing (685 docs). Whisper medium dual GPU chunking. Triple GPU pipeline. RAG query funcionando. NETFLICS Roku app 70% (BrightScript + Jellyfin backend). Navidrome deployed (:4533).

**30 Mar** — RAG Pipeline v2.0: SRT parsing (1.545 chunks Alive! Animation em 5 min vs 3-6h Whisper). ChromaDB: 3.378 → 6.814 docs.

**31 Mar** — Creative Director RAG pipeline criado.

---

## Abril 2026 — Week 1: RAG Full Library

**02 Apr** — Fix Ollama connection (192.168.68.112 → 172.17.0.1). RAG API multi-collection. Creative Director dual mode (CD + TD). Anti-alucinação implementada. Decision: qwen2.5:32b é modelo de produção.

**03 Apr** — 174 livros organizados em 13 categorias. 48.401 chunks indexados com category. 65k chunks antigos deletados. Kiwix Wikipedia 49GB deployed (:8888). 11 pipelines RAG operacionais. Knowledge RAG Full Library funcional (cita fontes reais). English Tutor + Design Tutor functional.

**04 Apr** — Cinematography RAG dedicado. Vision RAG (frame → análise → RAG técnico). Frame Star Wars testado → tutorial Blender EEVEE gerado. 10 pipelines testados e documentados.

**05 Apr** — knowledge_cinematography_v2: 11.261 chunks de 21 livros. RAG Matriz de Acesso documentada.

**06 Apr** — GitHub repos criados (homelab-core + homelab-ai-pipeline). Pipeline Guide documentado. Agent 01 + Agent 02 especificados. CEP Panel conceito.

---

## Abril 2026 — Week 2: Pipeline Audiovisual completo

**07 Apr** — Agent 3 (Narrativa + RAG), Agent 4 (Vision Color), Agent 8 (Post Mortem + MPV) functional. Full pipeline ran: 22m20s. Confidence Memória Projetual Viva: 0.5 → 0.62. MemPalace installed (138 drawers). Decision: pipeline delivers navigation, not prescription. MEMORABILIA name was born. Manifesto "O Pipeline como Organismo Vivo."

**08 Apr** — Agent 8: compress_aaak() com 7 types. client_summary.md por cenário. MEMORABILIA Status Card v5. Roadmap completo.

**09 Apr** — Ollama atualizado para 0.20.4. gemma4:26b a 53 t/s (vs 9.35 antes com qwen2.5:32b). 11 agents implementados. Visual Library v1.0. MusicGen audio guide. CEP Panel no Premiere Pro. DDV game trailer testado. Namespace architecture. Agent 4 + Agent 6 removidos — decisão arquitetural sem rough cut.

**10 Apr** — scene_frame_indexer v2.0: 4 modos adaptativos (arc/dual/single/window). 384 frames indexados. raw vs edited automático. knowledge_montagem: 4.260 chunks (Eisenstein, Tarkovsky, Bresson, Murch). Montagem RAG integrado. Memory Bible verificada. win_tools SMB montado. Decision: Agent 4 candidate_segments e Agent 6 suggested_cuts removidos permanentemente.

---

## Abril 2026 — Week 2: Design + CEP Graph + Obsidian

**11 Apr** — Auditoria de segurança: 27 fixes. UFW full sweep, DOCKER-USER chain, SSH MaxAuth 3, fail2ban. Risco ALTO → BAIXO.

**11 Apr** — Design Philosophy v1.0: 7 princípios documentados (Tradução de Tempo, Anti-Biblioteca, Desdobramento, Contexto Relacional, Amplificação, Paralelismo, Julgamento Acumulado). Inspiração: entrevista Andrea Trabuko (Pentagram).

**11 Apr** — Agent 3c redesenhado: Leitura Narrativa com Tensão Calibrada. Query dupla canônico/episódico, score de confiança, divergência explícita.

**11 Apr** — Agent 8 redesenhado: Memória Projetual Viva — Closer. Sugerido vs escolhido vs divergência, full relational context.

**11 Apr** — CEP v3 Spec: second brain do projeto (hyperlinks, tags editor, backlinks, aliases, embeds, bookmarks).

**11 Apr** — CEP Panel real (index.html): Graph View adicionado com force-directed SVG, thumbnails reais da API, sidebar esquerda estilo Obsidian (Filters/Groups/Display/Forces), sidebar direita com clip info + 4 botões de ação.

**11 Apr** — Obsidian installed no Linux (AppImage --no-sandbox). Vault criado em /media/pingpong/DATA/memorabilia-vault. Plugins: Templater, Dataview, Calendar. Template briefing YAML com campos mapeados aos agents. Primeiro projeto: DOC_VIDIGAL_2026.

**11 Apr** — Samba: share DATA adicionado. Obsidian acessível no Windows via \\192.168.68.113\DATA\memorabilia-vault.

**12 Apr** — API fix: int(float()) no timestamp_sec. extract_tags() para gerar tags da descrição em runtime. auto_tags na resposta de busca.

**12 Apr** — memorabilia-api.service: systemd + enable-linger (sobrevive reboot).

**12 Apr** — CEP Panel: 3 views finais (List, Grid, Graph). Cluster removido. SVG 4 layers (edges → themes → clip-bg → clips). Zoom/pan. Drag nodes. Busca principal funcional em todas as views. Grid/List drag swap.

**12 Apr** — 333 notas do Joplin exportadas para Obsidian vault em 10 categorias organizadas.

**12 Apr** — MEMORABILIA v9 compilado: documento de 2 páginas com filosofia integrada.

**12 Apr** — HomeLab Cluster Inventory: todos os devices da rede identificados (13 devices, 4 HomeLab, 4 mesh, 4 casa, 1 offline).

---

## Resumo — do zero em 34 days

| Week | Período | Marco |
|---|---|---|
| 0 | Jan 28 | First digital note |
| 1 | Mar 9–14 | Linux from zero (12 lições) |
| 2 | Mar 15–17 | Cloud + VPN + AI local (Phases 1-3 completas) |
| 3 | Mar 18–22 | Arquitetura + Pipeline design |
| 4 | Mar 23–28 | Pipeline v1 + SMB + Windows hardening |
| 5 | Mar 29–31 | RAG Pipeline (ChromaDB + 6.814 docs) |
| 6 | Apr 2–6 | RAG Full Library (48k chunks + 11 pipelines) |
| 7 | Apr 7–10 | Pipeline 11 agents + MEMORABILIA + MPV |
| 8 | Apr 11–12 | Design Philosophy + CEP Graph + Obsidian vault |

### Números finais (12 Abril 2026)

```
Pipeline:        9 agents · 50 min · 1 comando
Conhecimento:    72.263 trechos indexados
Memória:         105 entradas episódicas · 7 types
Visual Index:    384 frames · 4 modos adaptativos
Serviços:        20+ serviços ativos
Collections:     8 ChromaDB
Assistants:      6 especializados + 14 pipelines Open WebUI
CEP Panel:       3 views (List · Grid · Graph) no Premiere Pro
Obsidian:        333 notas organizadas · vault Linux + Windows
Segurança:       27 fixes · SSH key-only · fail2ban · UFW hardened
Hardware:        3 GPUs · 38GB VRAM · 208GB RAM · 20TB storage
Custo mensal:    $0
```

---

*pingpong · Montreal · April 12, 2026*
*MEMORABILIA · Timeline de Implementação v1 · 34 days do zero ao pipeline*
