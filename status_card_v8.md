# MEMORABILIA — Status Card v8

HomeLab pingpong · Montreal · April 12, 2026

---

## PINGPONG OS — 5 Módulos

| Módulo | Status | Existe hoje | Falta |
|---|---|---|---|
| SYSTEM | ⚠️ parcial | pipeline_launcher · watchdog_v2 · Frame.io CC · CEP panel · Obsidian vault | PocketBase · kanban · dashboard |
| DATA FLOW | ✅ funcional | Agents 1+2+3a+3b+3c+7+8+9 · watchdog 3 gatilhos | Flamenco |
| VISUAL LIBRARY | ❌ novo | spec documentada | PocketBase · frontend · /deck-brief |
| CINEMATOGRAPHER | ✅ funcional | ProblemSolver_v01 · RAG 11k chunks · montagem 4260 chunks · gemma4:26b | qwen3-vl UI integrada |
| TECHNICAL DIRECTOR | ✅ funcional | technical_director.py · RAG AI+Tech+Blender | Unity/Unreal/Math_VFX pendentes |

---

## Pipeline v8 — Fluxo Completo

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ENTRADA — VISUAL BIBLE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[project_brief.md]       Obsidian/Joplin · YAML frontmatter → pipeline
                         Template com campos mapeados aos agents
                         Vault: /media/pingpong/DATA/memorabilia-vault
[visual_library.py]      referências → deck_brief.json       ✅  4.5 min
[musicgen_guide.py]      brief + deck → audio_guide.wav      ✅  12 min
                         → copiado para 02_AUDIO/01_MIX/ automaticamente
[Cinematographer]        plano técnico iluminação             ✅  gemma4:26b + montagem RAG

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BLOCO 1 — PRÉ-EDIÇÃO (infraestrutura de navegação)
watchdog: footage AND brief → dispara
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Agent 1+2]  Ingest + Whisper large-v3     ✅  Windows RTX 4080
             → transcrição completa com timecodes
             → type:audio depositado

[Agent 3a]   Índice textual               ✅  HomeLab gemma4:26b · 1.5 min
             → full_transcript_index.md

[Agent 3b]   Visual Index — scene_frame_indexer v2.0
             ✅  Windows qwen3-vl
             → 4 modos adaptativos: arc / dual / single / window
             → raw (02_CAPTURES) e edited (03_EDITED) separados
             → 384 entries · material_type · rhythm_mode · cuts_per_minute

[Agent 3c]   Leitura Narrativa com Tensão Calibrada
             ✅  HomeLab gemma4:26b · 3 min
             → query dupla: canônico (livros) + episódico (projetos)
             → score de confiança por perspectiva (0.0–1.0)
             → divergência explícita quando > 0.3
             → referência a projetos anteriores similares
             → observações posicionadas, nunca prescrições
             REDESENHADO: v8.5 — duas perspectivas em tensão

DECISÃO ARQUITETURAL:
  Sem rough cut. Sem candidate_segments. Sem suggested_cuts.
  O pipeline entrega infraestrutura de navegação, não decisão criativa.
  O editor decide. O material é o autor.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HUMANO — Edição
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Premiere Pro + CEP MEMORABILIA
  → 3 views: List · Grid · Graph
  → busca visual semântica (384 frames · PT→EN · auto_tags)
  → busca textual (transcrição com timecodes)
  → marcadores de divergência (informação técnica · não prescrição)
  → thumbnails com timecodes clicáveis
  → Graph view: force-directed SVG com thumbnails reais
    sidebar esquerda estilo Obsidian (Filters/Groups/Display/Forces)
    sidebar direita (thumbnail, tags, descrição, 4 botões ação)
    zoom in/out (scroll wheel) · pan (Shift+drag)
    drag nodes · auto_tags extraídas da descrição
  → Grid/List: drag-and-drop swap para reordenar

C1  Edição imagens + MusicGen
C2  Edição + Motion Graphics (AE) + MusicGen
C3  Edição + Motion + 3D + ComfyUI híbrido + MusicGen
C4  Motion Graphics puro + MusicGen
C5  Motion + ComfyUI AI híbrido + MusicGen

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
BLOCO 2 — PÓS-EDIÇÃO
watchdog: render em 03_RENDER/02_OFF/ → dispara
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[Agent 7]    Vision + Color              ✅  qwen3-vl + gemma4:26b · 3 min
             → type:vision depositado

[Agent 6b]   SEO Metadata               ✅  gemma4:26b · 32 seg
             → legendas + descrições · 6 plataformas

[Agent 8]    Glasswing Closer            ✅  gemma4:26b · 3.5 min
             → postmortem.md · client_summary.md
             → compress_aaak() 7 types → ChromaDB
             → registra: sugerido vs escolhido vs divergência
             → por assistant, com confiança e condições do projeto
             → resumo para o cliente como subproduto
             → depósito relacional como produto principal
             REDESENHADO: v8.5 — contexto relacional completo

[Agent 9]    To Publish                  ✅  n8n webhook

Total máquina: ~50 min · Edição criativa: humano

♻️  Glasswing loop → episodic_memory → próximo projeto
```

---

## Design Philosophy — 7 Princípios

| # | Princípio | Teste |
|---|---|---|
| 1 | Tradução de Tempo | O agent transforma ou apenas copia? |
| 2 | Anti-Biblioteca | O output é encontrável por significado? |
| 3 | Desdobramento | O output gera múltiplas camadas de valor? |
| 4 | Contexto Relacional | O output carrega relação com o resto? |
| 5 | Amplificação | O output navega ou prescreve? |
| 6 | Paralelismo | O agent declara dependências e roda quando pode? |
| 7 | Julgamento Acumulado | O agent deposita algo que calibra o futuro? |

---

## CEP Panel — 3 Views

| View | Função | Interação |
|---|---|---|
| List | Flat, texto, metadata cruzada | Click para selecionar · drag swap para reordenar |
| Grid | Thumbnails lado a lado | Click para selecionar · drag swap para reordenar |
| Graph | Grafo relacional force-directed | Click=select · drag=move nó · scroll=zoom · Shift+drag=pan |

**Graph sidebar esquerda (estilo Obsidian):**
- Filters: busca + toggles (Temas/Links/Órfãos)
- Groups: campo @tag para filtrar por tags
- Display: sliders (Text fade/Node size/Link thickness)
- Forces: sliders (Center/Repel/Link/Distance)

**Graph sidebar direita (clip info):**
- Thumbnail · timecode · score · tags auto_tags
- Descrição visual · transcrição Whisper · observação Agent 3c
- Botões: Open in Source Monitor · Go to TC · + Marker · Copy TC

**CEP v3 Spec (second brain):**
- Tags do editor (#tag na busca) — nós coloridos no grafo
- Bookmarks (!select, !descarte) — anel dourado / opacidade 20%
- Links manuais (@clip) — arestas brancas com label
- Backlinks — tamanho do nó escala com conexões
- Aliases — múltiplos nomes por clip
- Embeds — hover preview inline

---

## Obsidian Vault — Second Brain Global

```
/media/pingpong/DATA/memorabilia-vault/
├── Templates/project_brief.md    ← template YAML → pipeline
├── Projetos/DOC_VIDIGAL_2026.md  ← primeiro briefing
├── Referências/                  ← notas Samsung migradas
│   ├── Borges.md · MFA.md · Motion design perspective.md
│   └── TIME/
├── Arquivo/                      ← projetos finalizados (futuro)
└── Home.md                       ← índice do vault

Plugins: Templater · Dataview · Calendar
Acesso: Linux (AppImage --no-sandbox) · Windows (via Samba \\192.168.68.113\DATA)
Graph View: 3 nós conectados (Project brief → Montreal → Home)
Filtro: path:Projetos para ver só projetos
```

---

## Knowledge RAG — Collections

| Collection | Chunks | Dims | Conteúdo |
|---|---|---|---|
| knowledge_montagem | 4.260 | 768 | Eisenstein · Tarkovsky · Bresson · Murch · Truffaut · Henri · Eco · Rocha |
| knowledge | ~48.401 | 768 | 174+ livros gerais |
| knowledge_cinematography_v2 | 11.261 | 768 | 21 livros reais de cinematografia |
| knowledge_cinematography | 649 | 384 | Brejon CG — NÃO MODIFICAR |
| tutorials | ~7.868 | 768 | 14 cursos |
| visual_library | 6 | 768 | imagens referência |
| visual_index | 384 | 768 | frames · scene_frame_indexer v2.0 · 4 modos |
| episodic_memory | ~105 | 768 | memória HomeLab + projetos · 7 types |

---

## Glasswing Memory — 7 Types

```
episodic_memory ChromaDB (768 dims)
    ├── type: narrative
    ├── type: audio
    ├── type: vision
    ├── type: motion      ← Cenários 2, 3, 4, 5
    ├── type: generative  ← Cenários 3, 5
    ├── type: 3d          ← Cenário 3
    └── type: project
```

---

## Infraestrutura

| Serviço | Porta | Status |
|---|---|---|
| Ollama HomeLab | 11434 | ✅ 0.20.4 · gemma4:26b · 53 t/s |
| Ollama Windows | 11434 | ✅ 0.6.8 · qwen3-vl:8b · 100% GPU |
| ChromaDB | 8000 | ✅ 8 collections · 105 episodic entries |
| RAG API | 8500 | ✅ McKee · Field · Block · /search_montagem |
| Visual Search API | 8700 | ✅ systemd + enable-linger · dual-lang PT→EN · auto_tags |
| Open WebUI | 3000 | ✅ 14 pipelines |
| n8n | 5678 | ✅ Docker |
| memory_manager | 8502 | ✅ |
| SMB win_tools | /mnt/win_tools | ✅ D:\TOOLS\ montado via CIFS |
| SMB DATA | /media/pingpong/DATA | ✅ Samba share · Obsidian vault |
| Obsidian | AppImage | ✅ Linux + Windows via Samba |
| PocketBase | 8090 | ❌ instalar |
| Flamenco Manager | 8080 | ⏳ Julho 2026 |

---

## Documentação produzida — April 11-12

| Documento | Conteúdo |
|---|---|
| MEMORABILIA v9 | Documento compilado 2 páginas — pipeline + filosofia |
| Design Philosophy v1.0 | 7 princípios + refinamento agents + prioridades |
| CEP v3 Spec | Second brain — hyperlinks, tags, bookmarks, aliases, embeds |
| project_brief_template.md | Template Obsidian/Joplin com YAML → pipeline |

---

## Gotchas Críticos

```
🔴 evalScript Premiere 2025+ REQUER callback (sync retorna undefined)
🔴 createMarker aceita SEGUNDOS direto, não ticks
🔴 Após update Ollama: verificar override.conf (OLLAMA_MODELS/HOST/NO_CLOUD)
🔴 Videos editados → 03_EDITED · Videos brutos → 02_CAPTURES (separação obrigatória)
🔴 Obsidian AppImage requer --no-sandbox no Ubuntu 24 (SUID sandbox error)
🔴 visual_search_api.py: timestamp_sec vem como float string — usar int(float())
🔴 extract_tags() DEVE estar definida ANTES da função search() no arquivo
🔴 SVG opacity no <g> afeta TODOS os filhos — backgrounds sólidos em layer separada
🔴 Docker bypassa UFW — DOCKER-USER chain em /etc/ufw/after.rules

🟡 gemma4:26b precisa num_predict 4000 (thinking tokens contam)
🟡 RAG queries em inglês — nomic-embed treinado em EN
🟡 qwen3-vl NÃO suporta num_predict — retorna vazio silenciosamente
🟡 Imagens > 1280px causam timeout no vision model
🟡 ollama.embeddings() não aceita host= — usar ollama.Client(host=)
🟡 ChromaDB visual_index não tem rhythm_mode/material_type — usar extract_tags()
🟡 Obsidian vault via Samba: plugins podem dar "failed to load" — ignorar
🟡 Grid/List drag: splice+insert faz cascade — usar swap para troca direta
🟡 Mistral tradução é gargalo da busca (~5-10s) — considerar skip para EN
🟡 Graph: onClick do SVG bg cancela seleção do node — usar ref flag
```

---

*pingpong · Montreal · April 12, 2026*
*MEMORABILIA · Pipeline Audiovisual v8 · Status Card*
