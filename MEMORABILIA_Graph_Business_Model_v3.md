---
projeto: MEMORABILIA Graph
tipo: business-model-plugin
data: 2026-04-13
versao: v3
status: atual
---

# MEMORABILIA Graph — Conceito & Modelo de Negócio v3

Plugin Second Brain para Editores de Vídeo
pingpong · Montreal · April 2026

---

## 1. O Problema

Editores de vídeo trabalham com timelines. Timelines são lineares. O pensamento narrativo não é.

Um editor recebe 20 horas de footage de um documentário. Precisa encontrar o momento em que a entrevistada hesita antes de falar do pai. Precisa lembrar que aquele B-roll do mercado dialoga com outro B-roll da praia filmado 3 dias depois. Precisa marcar os 40 clips aprovados entre os 300 disponíveis. Precisa saber que este projeto tem estrutura similar ao último e que certas decisões funcionaram.

Hoje, tudo isso mora na cabeça do editor. Quando o projeto fecha, evapora. Quando o editor sai, o conhecimento vai junto. Quando o projeto reabre 6 meses depois, recomeça do zero.

Nenhuma ferramenta de edição oferece uma camada de pensamento narrativo sobre o footage. Bins organizam por pasta. Metadata organiza por campo técnico. Ninguém organiza por significado.

---

## 2. A Solução

**MEMORABILIA Graph** é um plugin que adiciona uma camada de grafo relacional ao Premiere Pro e DaVinci Resolve. Cada clip vira um nó visual. Relações entre clips viram arestas. O editor externaliza o pensamento narrativo que antes ficava apenas na cabeça — e o sistema preserva entre sessões, entre projetos, entre equipes.

**Pitch:** Obsidian Graph View para editores de vídeo — vê relações entre clips que nenhuma timeline mostra.

**Princípio:** O editor é o motor semântico. O plugin é a tela. Sem AI, sem cloud, sem setup.

### Antes vs Depois

| Tarefa | Sem plugin | Com plugin |
|---|---|---|
| Encontrar clip específico | Navega bins · assiste footage | Busca por tag, metadata ou texto |
| Lembrar relações entre clips | Memória pessoal | Grafo visual com links explícitos |
| Marcar aprovados/rejeitados | Markers ou bins separados | !select / !descarte com visual no grafo |
| Agrupar clips por tema | Bins manuais | #tag cria grupo no grafo instantaneamente |
| Reabrir projeto antigo | Reassistir footage | Second brain intacto — tags, links, bookmarks |
| Passar projeto para outro editor | Briefing verbal | Grafo com contexto narrativo completo |
| Cross-reference entre clips | Mental ou notas externas | @link com label visível no grafo |

---

## 3. Como Funciona

### 3 Views sincronizadas

**List** — scan rápido com filename, timecode, tags e transcrição inline. Drag para reordenar.

**Grid** — thumbnails com frame real do clip. Badges de tag e score. Drag swap para reordenar. Exploração visual.

**Graph** — grafo relacional force-directed. Cada clip é um nó circular com a imagem do frame. Temas automáticos (câmera, frame rate, data, locação GPS) como nós menores conectando clips relacionados. Tags do editor como nós coloridos. Links manuais como arestas brancas com label.

Seleção, tags e bookmarks persistem entre as 3 views.

### Edges automáticas (sem AI)

O plugin gera relações automaticamente a partir da metadata nativa — sem AI, sem processamento pesado:

- Mesmo reel / mesmo take → aresta forte (weight 1.0)
- < 5 min entre clips (timestamp) → aresta temporal (weight 0.8)
- Mesma câmera → aresta via nó tema (weight 0.5)
- Mesmo GPS < 50m → aresta locação (weight 0.7)
- Mesmo frame rate → aresta técnica (weight 0.3)
- Mesmo scene/take → aresta forte (weight 1.0)

Fonte: Native metadata extraction. Formatos suportados: MP4, MOV, MXF, ProRes, DNxHD, H.264, H.265, RAW.

### Busca = criação

A barra de busca é input de busca e de criação ao mesmo tempo:

- Texto livre → busca por filename, metadata, tags
- `#entrevista-maria` → cria ou filtra tag (nó colorido no grafo)
- `!select` → marca como aprovado (anel dourado)
- `!descarte` → marca como rejeitado (opacidade 20%)
- `@clip-042` → cria link manual com label entre clips
- Combinações: `#entrevista AND drone` → clips com ambas tags

### Persistência

JSON salvo ao lado do arquivo de projeto (.prproj / .drp):

*(JSON schema — proprietary)*

- Reabre o projeto 6 meses depois → second brain intacto
- Exporta tags de um projeto para outro (cross-project memory)
- Backup automático do JSON a cada save
- Undo/redo para tags e links (10 níveis)

### Stack técnica

**Premiere Pro:** NLE Extension · NLE integration layer · Metadata engine · Force-directed graph engine · JSON local ao lado do .prproj

**DaVinci Resolve:** Companion app standalone (Desktop framework) · DaVinci API Python/Lua · MediaPool + Timeline + Markers · Mesma engine de grafo · Same persistence layer

**Shared:** Metadata extraction · Camera metadata extraction · JSON schema compartilhado · SVG force-directed graph engine

---

## 4. Roadmap de Implementação

### Fase 0 — Fundação (2 semanas)
- JSON schema v1.0
- Metadata parser (qualquer formato)
- Camera metadata parser (camera EXIF/XMP)
- Edge generator automático v1.0 (6 regras baseadas em metadata)
- Testes com footage real

### Fase 1 — Premiere Pro MVP (3 semanas)
- Extension scaffold
- Leitura de clips do projeto Premiere
- Integrar FFprobe como processo externo
- JSON persistência ao lado do .prproj
- Graph View engine (adaptar do CEP existente)
- Sidebars (controles + clip info)
- Tag system (#tag, !select, !descarte, @clip)
- Multi-select + 3 views sincronizadas

### Fase 2 — Refinamento (2 semanas)
- Smart edges (regras aprendidas do editor)
- Timeline markers bidirecional (tags ↔ markers Premiere)
- Busca avançada (metadata + data range + duração + câmera)
- Performance (lazy loading, Web Workers, cache thumbnails, 500+ clips)
- Import/Export (CSV, Premiere sequence, cross-project, SVG/PNG)
- Keyboard shortcuts (T/L/S/D/1/2/3/Ctrl+F)
- Persistência cross-session com undo/redo

### Fase 3 — DaVinci Resolve (3 semanas)
- Companion app standalone (Desktop framework)
- Resolve ↔ Graph sync via Python script
- Mesma UI adaptada para standalone (window management, hotkeys)
- Testes com projetos reais + edge cases

### Fase 4 — Produto (2 semanas)
- Installers (extension package Premiere, .dmg/.exe/.AppImage DaVinci)
- Documentação (quick start, video tutorial, FAQ)
- Landing page com demo video
- Beta program (10 editores)
- Soft launch (Reddit, Product Hunt, YouTube, aescripts.com)

```
     Abr          Mai          Jun          Jul
  ├──────────┼──────────┼──────────┼──────────┤
  │ Fase 0   │ Fase 1   │ Fase 2   │ Fase 3+4│
  │ Schema   │ Premiere │ Polish   │ DaVinci │
  │ FFprobe  │ MVP      │ Smart    │ Product │
  │ 2 sem    │ 3 sem    │ 2 sem    │ 5 sem   │
  └──────────┴──────────┴──────────┴──────────┘
```

---

## 5. Mercado

### TAM / SAM / SOM

- **TAM:** ~5.7M editores profissionais (3.7M Premiere + 2M DaVinci)
- **SAM:** ~855k editores com projetos de 50+ clips (15% do TAM)
- **SOM Year 1:** ~4.275 editores que buscam ferramentas de organização (0.5% do SAM)

### 4 Personas

- **Editor Freelancer** — 3-5 proj/mês, 5-30 clips. Dor: reabrir projetos sem contexto. Tier: FREE → PRO
- **Editor de Documentário** — 1-3 proj longos/ano, 200-2000 clips. Dor: encontrar momentos em centenas de horas. Tier: PRO
- **Post House / Studio** — 5-20 editores, 10-30 proj/mês. Dor: passagem de projeto entre editores. Tier: PRO → MEMORABILIA
- **Editor YouTube/Social** — alto volume, footage curto. Dor: templates reutilizáveis. Tier: FREE

### Competidores e Gap

| Produto | O que faz | O que NÃO faz | Preço |
|---|---|---|---|
| Frame.io | Review + aprovação por timecode | Navegação narrativa, grafo, tags persistentes | $15-30/user/mês |
| Kyno | Ingest, preview, metadata | Grafo relacional, links entre clips | $139 one-time |
| Silverstack | On-set DIT, backup, QC | Edição, navegação narrativa | $299-999 |
| PostLab | Colaboração, versionamento | Second brain, grafo, tags narrativas | $9-49/user/mês |
| Hedge (EditReady) | Transcode, checksum | Tudo acima | $99-199 |
| Lumberjack System | Logging de entrevistas | Grafo, links, multi-format | $199/ano |

**Gap:** nenhum produto oferece grafo relacional para clips de vídeo. O conceito de second brain para footage não existe como produto.

---

## 6. Modelo de Receita

### 3 Tiers

**FREE** — 50 clips · 3 views · tags + bookmarks · metadata automática · 1 projeto · sem links manuais · sem export. Objetivo: validar conceito, crescer user base.

**PRO ($49 USD one-time)** — Clips ilimitados · links manuais com labels · smart edges · import/export tags · cross-project memory · projetos ilimitados · Premiere + DaVinci · keyboard shortcuts · timeline markers sync. Objetivo: receita principal.

**MEMORABILIA ($199 USD one-time)** — Tudo do PRO + integração AI pipeline · auto-tags via AI · busca semântica por descrição · memória projetual viva entre projetos · Semantic search integration · 6 assistants especializados. Objetivo: upsell editor-técnico.

### Por que one-time

1. Editores odeiam subscriptions (Adobe backlash). One-time é diferencial competitivo.
2. Switching cost orgânico: 200 tags + 50 links = editor não troca. Retenção pelos dados, não pela cobrança.
3. Upgrades pagos por major version (v1→v2: $29 PRO, $99 MEMORABILIA). Receita recorrente sem subscription.
4. Venda direta = 0% comissão + Stripe 2.9%. aescripts.com = 30%.

### Projeção

| Ano | Downloads | Conversão PRO | Conversão MEMORABILIA | Receita Total |
|---|---|---|---|---|
| Year 1 | 5k-10k free | 400-800 ($49) | 100-200 ($199) | $39k-79k USD |
| Year 2 | 15k-30k | 1.2k-2.4k + upgrades v2 | 300-600 | $80k-160k USD |
| Year 3 | 40k-80k | acumulado + Team tier | acumulado | $150k-300k USD |

Custos: dev $0 (solo), hosting $0 (GitHub Pages), Stripe 2.9%. **Margem: 87-95%.**

---

## 7. Go-to-Market

### Fase 1 — Seed
- Landing page com demo video (30s GIF + 2min full)
- Email waitlist (ConvertKit free)
- Reddit teaser: "I built an Obsidian-style graph view for video editors"
- Twitter/X: demo GIF 15s loop (viral potential alto — conceito visual novo)
- 3 beta testers: documentarista, freelancer, post house

### Fase 2 — Launch
- Product Hunt: "Obsidian Graph View for Video Editors"
- YouTube tutorial 5 min (self-produced)
- Reddit launch posts com caso de uso real
- Outreach YouTube channels: Film Riot, Premiere Gal, Casey Faris, JayAreTV
- aescripts.com listing (marketplace Adobe)

### Fase 3 — Growth
- Case studies de beta testers
- Blog posts SEO: "How I organized 2000 clips"
- Discord community
- Feature requests votados pela community
- Affiliate program 20% por venda

### Canais

| Canal | Comissão | Vantagem |
|---|---|---|
| Site direto + Stripe | 2.9% | Margem máxima |
| aescripts.com | 30% | Marketplace Adobe, visibilidade |
| Gumroad | 5% | Simple, indie-friendly |

---

## 8. O que já está implementado

### Pronto (40% do código)

- ✅ Graph View engine SVG force-directed — implementado no CEP
- ✅ 3 views sincronizadas (List/Grid/Graph) — implementado
- ✅ Sidebar esquerda Obsidian-style — implementado
- ✅ Sidebar direita clip info + 4 botões — implementado
- ✅ Zoom/pan/drag — implementado
- ✅ CEP Extension structure — funcionando no Premiere
- ✅ Premiere ExtendScript (Source Monitor, markers, timecodes)
- ✅ Tag system (#tag) — especificado no CEP v3
- ✅ Bookmark system (!select/!descarte) — especificado
- ✅ Link system (@clip) — especificado
- ✅ Filosofia de design (7 princípios)
- ✅ Experiência com footage real (3 projetos testados)

### Falta construir

- ⬜ Metadata parser para metadata nativa
- ⬜ Edge generator baseado em metadata (não AI)
- ⬜ JSON schema v1.0 + persistência cross-session
- ⬜ Smart edges (regras aprendidas)
- ⬜ DaVinci Resolve companion app
- ⬜ Packaging para distribuição

---

## 9. Riscos e Mitigações

| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Adobe mata CEP | Média | Alto | Migrar UXP (já funciona). Timeline: 2027+ |
| Ninguém paga $49 | Baixa | Alto | Free tier valida. Ajustar preço se conversão < 3% |
| Competidor copia | Média | Médio | First mover + community + velocidade solo |
| Performance 1000+ clips | Média | Médio | Clustering + lazy loading + Web Workers |
| DaVinci API limitada | Alta | Baixo | Companion app standalone |
| Editor não entende conceito | Média | Alto | Demo 30s mostra antes/depois. Visual vende. |

---

## 10. Propriedade Intelectual

**Código proprietário:** Graph View engine, edge generator, JSON schema, tag/link system, CEP/UXP architecture, DaVinci companion app.

**Design proprietário:** 3 views com busca = criação, sidebar Obsidian-style para NLE, conceito "editor como motor semântico", conceito "second brain para footage".

**Proteção:** Copyright automático (Berne Convention) + Trademark MEMORABILIA Graph via CIPO (~$530 CAD, 12-18 meses). EULA: licença perpétua para versão comprada, sem redistribuição.

---

## 11. Expansão

- v1.0 — Premiere Pro + DaVinci Resolve
- v1.5 — Final Cut Pro (se demanda)
- v2.0 — AI layer (auto-tags, busca semântica) = MEMORABILIA upgrade
- v2.5 — Team features (shared graphs, multi-editor)
- v3.0 — Standalone app (funciona sem NLE, qualquer pasta de footage)
- v3.5 — Mobile companion (review grafo no celular/tablet)
- v4.0 — API para integração com DAMs (Iconik, Catdv, MediaSilo)

---

## Dois produtos, uma filosofia

**MEMORABILIA Graph ($49)** — Plugin standalone. Editor é o motor semântico. Metadata nativa + tags manuais. Zero setup, zero AI, zero cloud. Mercado: todos os editores.

**MEMORABILIA ($199)** — Pipeline completo. AI é o motor semântico + editor refina. 72k trechos + memória projetual viva. HomeLab + pipeline + agents. Upgrade do Graph.

O plugin valida o conceito. O pipeline é o upgrade para quem quer automação. O plugin é a entrada. O pipeline é o destino.

---

*pingpong · Montreal · April 13, 2026 · MEMORABILIA Graph · Conceito & Modelo de Negócio v3*
