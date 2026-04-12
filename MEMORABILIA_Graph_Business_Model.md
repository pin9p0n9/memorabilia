---
projeto: MEMORABILIA Graph
tipo: business-model
data: 2026-04-12
tags:
  - plugin
  - produto
  - business
  - premiere
  - davinci
status: draft-v2
---

# MEMORABILIA Graph — Conceito & Modelo de Negócio

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

### O que o editor faz hoje vs com o plugin

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

- Mesmo reel / mesmo take → aresta forte
- < 5 min entre clips (timestamp) → aresta temporal
- Mesma câmera → aresta via nó tema
- Mesmo GPS < 50m → aresta locação
- Mesmo frame rate → aresta técnica
- Mesmo codec / color space → aresta técnica

Fonte: FFprobe (container metadata) + ExifTool (camera EXIF/XMP).

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

```
meu_projeto_graph.json
├── clips: [{id, filename, metadata, tags, links, bookmarks}]
├── tags: {"#mercado": {color:"#5eead4", clips:[...]}}
├── links: [{from, to, label, created}]
├── bookmarks: {select:[], descarte:[], custom:{}}
└── version: "1.0"
```

- Reabre o projeto 6 meses depois → second brain intacto
- Exporta tags de um projeto para outro (cross-project memory)
- Backup automático do JSON a cada save
- Undo/redo para tags e links (10 níveis)

---

## 4. Mercado

### TAM / SAM / SOM

```
TAM (Total Addressable Market):
  ~3.7 milhões de editores de vídeo profissionais globalmente
  (Adobe reportou 3M+ creative professionals usando Premiere em 2025)
  + ~2M usuários DaVinci Resolve (Blackmagic reportou crescimento)
  = ~5.7M editores potenciais

SAM (Serviceable Available Market):
  Editores que trabalham com projetos de 50+ clips
  e sentem a dor de organização narrativa
  ~15% do TAM = ~855k editores

SOM (Serviceable Obtainable Market — Year 1):
  Editores que ativamente buscam ferramentas de organização
  e frequentam comunidades online (Reddit, Twitter, YouTube)
  ~0.5% do SAM = ~4.275 editores

  Conversão free → pro: ~8-12%
  = 340-510 licenças PRO no Year 1
  = $16.600-24.990 USD receita Year 1 (só plugin PRO)
```

### Personas

**Editor Freelancer** — trabalha sozinho, 3-5 projetos/mês, footage de 5-30 clips por projeto. Dor: reabrir projetos antigos sem contexto. Solução: tags e bookmarks persistentes. Tier: FREE → PRO.

**Editor de Documentário** — equipe pequena, 1-3 projetos longos/ano, footage de 200-2000 clips por projeto. Dor: encontrar momentos específicos em centenas de horas. Relações narrativas complexas. Solução: grafo + links + cross-reference. Tier: PRO.

**Post House / Studio** — 5-20 editores, 10-30 projetos/mês. Dor: passagem de projeto entre editores sem perder contexto narrativo. Solução: JSON exportável + memória cross-project. Tier: PRO → MEMORABILIA.

**Editor de YouTube/Social** — alto volume, 10-20 vídeos/mês, footage curto. Dor: templates de organização reutilizáveis. Solução: tags template exportáveis. Tier: FREE.

### Competidores e adjacentes

| Produto | O que faz | O que NÃO faz | Preço |
|---|---|---|---|
| Frame.io | Review + aprovação por timecode | Navegação narrativa, grafo, tags persistentes | $15-30/user/mês |
| Kyno | Ingest, preview, metadata | Grafo relacional, links entre clips | $139 one-time |
| Silverstack | On-set DIT, backup, QC | Edição, navegação narrativa | $299-999 |
| PostLab | Colaboração, versionamento | Second brain, grafo, tags narrativas | $9-49/user/mês |
| Hedge (EditReady) | Transcode, checksum | Tudo acima | $99-199 |
| Lumberjack System | Logging de entrevistas | Grafo, links, multi-format | $199/ano |

**Gap no mercado:** nenhum produto oferece grafo relacional para clips de vídeo. Zero. O conceito de second brain aplicado a footage não existe como produto.

---

## 5. Modelo de Receita

### Tiers

```
┌─────────────────────────────────────────────────────────────┐
│ FREE                                                         │
│ 50 clips · 3 views · tags + bookmarks · metadata automática │
│ 1 projeto · sem links manuais · sem export                  │
│                                                              │
│ Objetivo: validar o conceito, crescer user base, reviews    │
└──────────────────────────┬──────────────────────────────────┘
                           │ upgrade $49 USD
┌──────────────────────────▼──────────────────────────────────┐
│ PRO — $49 USD one-time                                       │
│ Clips ilimitados · links manuais com labels                  │
│ Smart edges · import/export tags · cross-project memory      │
│ Projetos ilimitados · Premiere + DaVinci                     │
│ Keyboard shortcuts completos · timeline markers sync         │
│                                                              │
│ Objetivo: receita principal, editor profissional             │
└──────────────────────────┬──────────────────────────────────┘
                           │ upgrade $199 USD
┌──────────────────────────▼──────────────────────────────────┐
│ MEMORABILIA — $199 USD one-time                              │
│ Tudo do PRO + integração AI pipeline                         │
│ Auto-tags via AI (sunset, crowd, medium shot)                │
│ Busca semântica por descrição natural                        │
│ Memória projetual viva entre projetos                        │
│ ChromaDB integration · 6 assistants especializados           │
│                                                              │
│ Objetivo: upsell para editor-técnico, margem alta            │
└─────────────────────────────────────────────────────────────┘
```

### Por que one-time e não subscription

1. **Editores odeiam subscriptions.** A community é vocal sobre isso (Adobe backlash). One-time é diferencial competitivo.
2. **Switching cost orgânico.** Uma vez que o editor tem 200 tags e 50 links num projeto, não troca de ferramenta. A retenção vem dos dados, não da cobrança.
3. **Upgrades pagos por major version.** v1 → v2 com features significativas = upgrade pago ($29 PRO, $99 MEMORABILIA). Receita recorrente sem subscription.
4. **Plugin marketplace comissão.** aescripts.com cobra 30%. Venda direta pelo site = 0% comissão + Stripe 2.9%.

### Projeção Year 1-3

```
YEAR 1 — Validação
  Downloads free: 5.000-10.000
  Conversão pro: 8% = 400-800 licenças
  Receita PRO: $19.600-39.200 USD
  Conversão MEMORABILIA: 2% = 100-200
  Receita MEMORABILIA: $19.900-39.800 USD
  ────────────────────────────────
  Receita total Year 1: $39.500-79.000 USD
  Custos: hosting site ($50/mês) + Stripe fees (~3%)
  Margem: ~95%

YEAR 2 — Crescimento
  Base free acumulada: 15.000-30.000
  Novas conversões pro: 1.200-2.400
  Upgrade v2 (existentes): 30% = 120-240
  Receita total: $80.000-160.000 USD

YEAR 3 — Maturidade
  Base free acumulada: 40.000-80.000
  Receita anual: $150.000-300.000 USD
  Possibilidade: Team tier ($199/seat/ano) para post houses
```

---

## 6. Go-to-Market

### Fase 1 — Seed (antes do lançamento)

```
[ ] Landing page com demo video (30s GIF + 2min full)
[ ] Email waitlist (ConvertKit free tier)
[ ] Reddit teaser posts:
    r/editors · r/premiere · r/davinciresolve · r/VideoEditing
    "I built an Obsidian-style graph view for video editors"
    → link para waitlist, não para produto
[ ] Twitter/X: demo GIF (15s, loop, sem áudio)
    → viral potential alto (conceito visual novo)
[ ] 3 beta testers: documentarista, freelancer, post house
```

### Fase 2 — Launch

```
[ ] Product Hunt launch
    → "Obsidian Graph View for Video Editors"
    → categoria: Productivity + Video
[ ] YouTube tutorial (5 min) — self-produced
[ ] Reddit launch posts com caso de uso real
[ ] Outreach para YouTube channels:
    → Film Riot, Premiere Gal, Casey Faris, JayAreTV
    → oferecer licença grátis em troca de review
[ ] aescripts.com listing (marketplace Adobe)
```

### Fase 3 — Growth

```
[ ] Case studies de beta testers publicados
[ ] Blog posts: "How I organized 2000 clips" (SEO)
[ ] Discord community para users
[ ] Feature requests votados pela community
[ ] Parceria com editores influencers
    → affiliate 20% por venda
```

### Canais de distribuição

| Canal | Comissão | Vantagem |
|---|---|---|
| Site direto + Stripe | 2.9% | Margem máxima, controle total |
| aescripts.com | 30% | Marketplace Adobe, visibilidade, confiança |
| Gumroad | 5% | Simple, indie-friendly |

**Estratégia:** lança no site direto primeiro (margem). Depois lista no aescripts.com (volume). Gumroad como backup.

---

## 7. Propriedade Intelectual

### O que é proprietário

```
CÓDIGO:
  Graph View engine (SVG force-directed customizado)
  Edge generator baseado em metadata nativa
  JSON schema de persistência cross-project
  Tag/Link/Bookmark system integrado à busca
  CEP/UXP Extension architecture
  DaVinci companion app architecture

DESIGN:
  3 views sincronizadas com busca = criação
  Sidebar Obsidian-style para NLE
  Conceito "editor como motor semântico"
  Conceito "second brain para footage"

BRAND:
  MEMORABILIA Graph (nome)
  Visual identity (paleta, tipografia)
  Demo video e materiais de marketing
```

### Proteção

```
[ ] Copyright automático (Berne Convention) — código e design
[ ] Trademark MEMORABILIA Graph — registro Canada (CIPO)
    Custo: ~$330 CAD (filing) + ~$200 CAD (registration)
    Tempo: 12-18 meses
[ ] Licença de uso no produto (EULA)
    → one-time purchase = licença perpétua para versão comprada
    → sem redistribuição do código
[ ] Open source parcial?
    → Graph engine como MIT (atrai community)
    → Integration layer como proprietário (monetiza)
    Decisão: avaliar após Year 1
```

---

## 8. Custos Operacionais

```
DESENVOLVIMENTO (Year 1):
  Desenvolvedor: $0 (tu — solo)
  Tempo: 12 semanas part-time (entre projetos)
  Hardware: já existe (HomeLab)
  Software: grátis (VS Code, Git, FFprobe, ExifTool)
  ────────────────────────────
  Total dev: $0

OPERACIONAL MENSAL:
  Domínio: ~$15/ano
  Hosting (landing page): $0 (GitHub Pages)
  Email (ConvertKit): $0 (free até 1000 subscribers)
  Stripe: 2.9% + $0.30 por transação
  aescripts.com: 30% por venda (se listar)
  ────────────────────────────
  Total fixo: ~$2/mês (domínio)
  Total variável: ~3-30% por venda (canal)

MARGEM:
  Venda direta: ~95%
  Via aescripts: ~67%
  Média ponderada (70/30 direto/aescripts): ~87%
```

---

## 9. Riscos e Mitigações

| Risco | Probabilidade | Impacto | Mitigação |
|---|---|---|---|
| Adobe mata CEP | Média | Alto | Migrar para UXP (já funciona). Timeline Adobe: 2027+ |
| Ninguém paga $49 | Baixa | Alto | Free tier valida. Se conversão < 3%, ajustar preço ou features |
| Competidor copia | Média | Médio | First mover. Community. Velocidade de iteração solo |
| Performance 1000+ clips | Média | Médio | Clustering + lazy loading + Web Workers |
| DaVinci API limitada | Alta | Baixo | Companion app standalone resolve |
| Editor não entende o conceito | Média | Alto | Demo video de 30s mostra o antes/depois. Visual vende |

---

## 10. Métricas de Sucesso

### Year 1

```
VALIDAÇÃO:
  [ ] 5.000+ downloads free
  [ ] 300+ licenças PRO vendidas
  [ ] NPS > 40 (survey in-app)
  [ ] 3+ reviews em YouTube channels com 50k+ subs
  [ ] 1 case study documentário publicado

PRODUTO:
  [ ] < 5 bugs críticos reportados no primeiro mês
  [ ] < 3s load time com 500 clips
  [ ] < 1s tag/link creation
  [ ] 0 data loss (JSON persistence 100% confiável)

FINANCEIRO:
  [ ] Receita > $30.000 USD Year 1
  [ ] CAC < $5 USD (orgânico first)
  [ ] Margem > 85%
```

---

## 11. Expansão Futura

```
v1.0 — Premiere Pro + DaVinci Resolve
v1.5 — Final Cut Pro (se demanda)
v2.0 — AI layer (auto-tags, busca semântica) = MEMORABILIA upgrade
v2.5 — Team features (shared graphs, multi-editor)
v3.0 — Standalone app (funciona sem NLE, qualquer footage folder)
v3.5 — Mobile companion (review grafo no celular/tablet)
v4.0 — API para integração com DAMs (Iconik, Catdv, MediaSilo)

POSSÍVEL PIVOT:
  Se o plugin vende bem → empresa de ferramentas para editores
  Se o pipeline vende bem → consultoria de AI para studios
  Se os dois vendem → ecossistema MEMORABILIA
```

---

## Resumo Executivo

MEMORABILIA Graph é um plugin de $49 que resolve um problema que nenhuma ferramenta de edição resolve: organizar footage por significado, não por pasta. O conceito — grafo relacional para clips de vídeo — não existe no mercado. 40% do código já está implementado. O custo de desenvolvimento é zero (solo dev com hardware existente). A margem é 87-95%. O mercado potencial é 855k editores com a dor de organização narrativa. O produto valida o conceito do MEMORABILIA pipeline completo ($199), criando um funil natural de free → PRO → MEMORABILIA.

O plugin é a entrada. O pipeline é o destino.

---

*pingpong · Montreal · April 12, 2026*
*MEMORABILIA Graph · Conceito & Modelo de Negócio v2*
