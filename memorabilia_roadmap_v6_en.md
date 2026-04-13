# MEMORABILIA — Roadmap v5.0

HomeLab pingpong · Montreal · April 12, 2026
Operador: pingpong (Leo) · solo · Montreal

---

## Principle de implementação

Cada camada só é construída depois que a anterior está working in production with real projects. The pipeline delivers navigation infrastructure — the material speaks for itself. The creative decides. O sistema é desenhado em torno de 7 principles (Design Philosophy v1.0) e dois agentes centrais: Agent 3c (leitura com calibrated tension) e Agent 8 (Memória Projetual Viva — Closer com relational context).

---

## Estado real hoje

```
FUNCIONA EM PRODUÇÃO:
  Pipeline ~50 min · 1 comando
  Agents 1+2+3a+3b+3c+7+8+9
  CEP panel: 3 views (List · Grid · Graph)
    Graph: force-directed SVG · thumbnails reais · auto_tags
    Sidebar esquerda Obsidian-style · sidebar direita clip info
    Zoom/pan · drag nodes · busca funcional todas as views
    Grid/List: drag swap reorder
  visual_index: 384 entries · scene_frame_indexer v2.0 · 4 modos adaptativos
  knowledge_montagem: 4260 chunks · Eisenstein/Tarkovsky/Bresson/Murch
  montagem RAG integrado: Cinematographer + Agent 3c + rag_api
  episodic_memory: ~105 entries · 768 dims · 7 types
  Confiança MPV 0.75
  Obsidian vault: /media/pingpong/DATA/memorabilia-vault
    Template briefing YAML → pipeline · Graph View · Linux + Windows
  Visual Search API: systemd + enable-linger · auto_tags · extract_tags()
  Samba: DATA share adicionado · Obsidian acessível Windows
  session memory loop: session_start · log_episodic · session_close

DESIGN:
  Design Philosophy v1.0 — 7 principles documentados
  Agent 3c redesenhado — calibrated tension (canônico vs episódico)
  Agent 8 redesenhado — Memória Projetual Viva — Closer (suggested vs chosen vs divergence)
  CEP v3 Spec — second brain do projeto (tags, links, bookmarks, aliases)
  MEMORABILIA v9 — documento compilado 2 páginas

DECISÕES ARQUITETURAIS:
  ❌ Sem rough cut — Agent 4 + Agent 6 removidos
  ✅ Pipeline = infraestrutura de navegação
  ✅ scene_frame_indexer v2.0 — ritmo adaptativo · raw vs edited
  ✅ Separação 02_CAPTURES (raw) vs 03_EDITED obrigatória
  ✅ Graph view no CEP com auto_tags (sem metadata rico no ChromaDB)
  ✅ Obsidian como second brain global (entre projetos)
  ✅ CEP Cluster como second brain local (dentro do projeto)

TESTADO COM PROJETOS REAIS:
  260406_V_HOMELAB — documentário · PT · Vidigal + MTL
  Game trailer — AAA studio · motion graphics
  Béla Tarr Werckmeister — Cinematographer test
```

---

## Action Points — por horizonte

### AP-3 ✅ — episodic_entry + Memory Bible
Completed. 260406 com 7 types. Wake-up context verificado.

### AP-2 ✅ — audio_guide.wav → pasta correta
Completed. musicgen_guide.py v1.1.

### AP-10 ✅ — Design Philosophy + Agent redesign
Completed April 12. 7 principles. Agent 3c calibrated tension. Agent 8 Memória Projetual Viva — Closer.

### AP-11 ✅ — CEP Graph View + auto_tags
Completed April 12. Graph no Premiere. extract_tags() no API. Sidebar Obsidian-style.

### AP-12 ✅ — Obsidian vault + briefing template
Completed April 12. Vault no DATA. Template YAML. Acessível Linux + Windows.

---

### AP-5 — wake-up context nos assistants RAG
Esforço: 3-4h · Impacto: alto · Prazo: Maio 2026

### AP-13 — Re-indexar visual_index com metadata rico
Esforço: 2-3h · Impacto: alto · Prazo: Esta semana
```
Adicionar rhythm_mode, material_type, scene_duration ao ChromaDB na indexação.
Elimina necessidade de extract_tags() como fallback.
Graph do CEP ganha links reais baseados em metadata.
```

### AP-14 — Agent 3c calibrated tension no pipeline real
Esforço: 4-6h · Impacto: alto · Prazo: Abril
```
Implementar query dupla canônico/episódico com score.
Divergência explícita > 0.3.
Referência a projetos anteriores similares.
```

### AP-15 — Agent 8 depósito relacional no pipeline real
Esforço: 3-4h · Impacto: alto · Prazo: Abril
```
Sugerido vs escolhido vs divergência.
Condições do projeto (tipo, cliente, audiência, paleta, BPM).
Padrões detectados a partir de 3 ocorrências.
```

### AP-16 — CEP v3 second brain features
Esforço: 1-2 semanas · Prazo: Maio
```
P0: Tags do editor na busca (#tag) + multi-select
P1: Bookmarks (!select, !descarte) + nó colorido no grafo
P2: Links manuais entre clips (@) + labels
P3: Zoom hierárquico por tags
```

---

## 🔴 Esta semana — Abril 12–18

```
[ ] AP-13 — Re-indexar visual_index com metadata rico
[ ] AP-14 — Agent 3c calibrated tension (implementar no pipeline)
[ ] AP-15 — Agent 8 depósito relacional (implementar no pipeline)
[ ] AP-5 — wake-up context nos assistants RAG
[ ] Whisper batch: Unity · Unreal · Math for VFX
[ ] Reindexar Blender_GameAssets_Udemy
[ ] Syncthing no Windows para vault offline
```

---

## 🟡 Resto de Abril — semanas 3–4

```
Visual Bible — Sprint 1
  Sprint 1A — MusicGen integrado ao watchdog
  Sprint 1B — Visual Library MVP (PocketBase + FastAPI + frontend)
  Sprint 1C — Deck por projeto (/decks · deck_brief.json)

CEP Graph — testar nodes opacos (SVG layers fix)
Dataview dashboard no Obsidian
```

---

## 🟢 Maio 2026

```
AP-4 — LightRAG para knowledge RAG
AP-5 — Memory Bible em todos os assistants (com 3+ projetos)
AP-7 — Visual Library MVP
AP-16 — CEP v3 second brain (tags editor + bookmarks)
CEP Panel — Assistants no Premiere (FastAPI :8800)
Metadata + Remotion
```

---

## 🟢 Junho 2026

```
AP-6 — OpenSpace como runtime (se 2 projetos rodados)
Memory Bible com 3+ projetos — measure calibration
Creative Director RAG com motion completo (AE + C4D)
```

---

## 🔵 Julho 2026

```
AP-8 — Flamenco render farm (se demanda Cenário 3+5)
Technical Director module — Blender + AE orquestração
ComfyUI integrado ao watchdog
LoRA por cliente
```

---

## 🟣 Agosto 2026

```
AP-9 — PINGPONG OS Dashboard
Agent 9 — auto-publish YouTube + Vimeo
End-to-end validation (Cenário 1 + Cenário 3)
MPV com 5+ projetos: measure calibration
```

---

## Resumo por mês

| Mês | Foco | Entrega real |
|---|---|---|
| Abril | Agent 3c/8 refinados + visual_index metadata | Pipeline com calibrated tension · Graph com links reais |
| Maio | LightRAG · Memory Bible · Visual Library · CEP v3 | Second brain funcional · assistants calibrados |
| Junho | OpenSpace · Motion RAG · CEP assistants | Recovery automático · assistants no Premiere |
| Julho | Flamenco · Technical Director | Render farm · compositing pipeline (se demanda) |
| Agosto | Dashboard · validação end-to-end | Pipeline completo · MPV calibrada |

---

## O que não está no roadmap e por quê

- Rough cut XML — decisão arquitetural: pipeline não prescreve sequência
- Agent 4 candidate_segments — removido
- Agent 6 suggested_cuts — removido
- Brazil Mac Mini — sem hardware confirmado
- LoRA por cliente — Julho
- Hetzner VPS + site — Setembro, marketing
- Jitsi self-hosted — meet.jit.si cobre 100%
- DeerFlow — avaliado, decisão Junho

---

## Dependências críticas

```
AP-13 re-index      → independente (roda agora)
AP-14 Agent 3c      → independente (roda agora)
AP-15 Agent 8       → independente (roda agora)
AP-5 wake-up        → depende de 2 projetos no ChromaDB
AP-16 CEP v3        → depende AP-13 (metadata rico)
AP-4 LightRAG       → depende AP-3 + dados reais

Sprint 1B            → independente
  └→ Sprint 1C       → depende Sprint 1B

FastAPI :8800        → independente
  └→ CEP assistants  → depende :8800

Flamenco             → depende de demanda real (Cenário 3+5)
Dashboard            → depende de tudo acima
```

---

## Hardware prioritário

```
RTX 3090 24GB used ~$1.000 CAD → gemma4 full speed · ComfyUI 3x
Samsung 990 Pro 4TB ~$400 CAD  → resolve 2TB Windows HOT
IronWolf 8TB ~$120 CAD         → HomeLab DATA backup (SPOF · SMART 26.947h)
```

---

*pingpong · Montreal · April 12, 2026*
*MEMORABILIA · Roadmap v5.0 · solo operator*
