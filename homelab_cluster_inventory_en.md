# MEMORABILIA — HomeLab Cluster Inventory

pingpong · Montreal · April 12, 2026

---

## Network Local — 192.168.68.0/24 · SSID: XIMBICA (TP-Link Deco Mesh)

| IP | Nome | Device | Connection | Role |
|---|---|---|---|---|
| .1 | Router | TP-Link Deco (principal) | Gateway | Mesh controller |
| .100 | Ximbica | Samsung Galaxy | Wi-Fi 5G | Mobile · Joplin · VPN 10.0.0.3 |
| .101 | TY_WR | TP-Link Deco (satélite) | — | Mesh node |
| .102 | TY_WR | TP-Link Deco (satélite) | Wi-Fi 2.4G | Mesh node |
| .103 | MacBookPro | MacBook Pro M1 | Wi-Fi 5G | Field · mobile · ⏳ pending VPN |
| .104 | iPhone | iPhone (alguém da casa) | Wi-Fi 5G | Não faz parte do HomeLab |
| .105 | SAMBA | Windows PC | Wi-Fi 5G | Edição · render · RTX 4080 |
| .106 | wlan0 | TP-Link Deco (interface) | Wi-Fi 2.4G | Mesh backhaul |
| .107 | Galaxy-A54-5G | Celular da casa | Wi-Fi 5G | Não faz parte do HomeLab |
| .108 | HP6F8240 | HP DeskJet 3755 | Wi-Fi 2.4G | Printer |
| .110 | iRobot | Roomba | Wi-Fi 2.4G | Vacuum |
| .111 | wlan0 | TP-Link Deco (interface) | Wi-Fi 2.4G | Mesh backhaul |
| .113 | pingpong-All-Series | HomeLab Linux | Wired (Ethernet) | AI server · pipeline |

---

## WireGuard VPN — 10.0.0.0/24

| IP | Peer | Endpoint | Status |
|---|---|---|---|
| 10.0.0.1 | HomeLab Linux | (server) | Sempre on |
| 10.0.0.2 | Windows PC | 192.168.68.105:60354 | 9 dias atrás |
| 10.0.0.3 | Samsung / MacBook | 198.200.124.199:41601 | 6h atrás |

---

## HomeLab Linux — 192.168.68.113

### Hardware

| Componente | Spec |
|---|---|
| Motherboard | ASUS X99-A II |
| CPU | Intel Core i7-6800K @ 3.40GHz (6 cores / 12 threads) |
| RAM | 128GB DDR4 2400 MT/s · Quad-Channel · 8/8 slots |
| RAM modules | 4× 16GB Kingston + 4× 16GB Samsung |
| GPU 1 | NVIDIA GeForce GTX 1080 Ti — 11GB VRAM |
| GPU 2 | NVIDIA GeForce GTX 1080 Ti — 11GB VRAM |
| Boot | NVMe 465GB ext4 — system + Docker + active work |
| DATA | SATA HDD 1.8TB ext4 — Ollama models + projects + vault |
| BLACKBOX | Seagate Expansion 14.9TB USB NTFS — cold archive (shared with Windows E:) |
| Wi-Fi | ASUS USB-AC56 Dual Band (Realtek RTL8812AU) |
| Monitor | ASUS PB279Q 27" 4K UHD · DisplayPort 1.2 · 60Hz |
| OS | Ubuntu 24.04 LTS |

### Samba Shares (exportados)

| Share | Path | Uso |
|---|---|---|
| blackbox | /media/pingpong/BLACKBOX | Arquivo 16TB |
| tutorials | ? | Cursos |
| DATA | /media/pingpong/DATA | Vault Obsidian · projetos · pipeline |

### CIFS Mounts (importados do Windows)

| Mount | Share Windows | Uso |
|---|---|---|
| /mnt/win_projects | //192.168.68.105/projects | D:\01_PROJECTS |
| /mnt/win_hot | //192.168.68.105/footage_hot | Footage quente |
| /mnt/win_tools | //192.168.68.105/tools | D:\TOOLS\ |
| /mnt/win_chromadb | //192.168.68.105/RAG_chromadb | ChromaDB backup Windows |

### Docker Networks

| Network | Bridge | Containers |
|---|---|---|
| docker0 | 172.17.0.0/16 | 4 containers (.2, .3, .4, .5) |
| br-afec3095fff3 | 172.18.0.0/16 | 2 containers |
| br-7daa2145de48 | 172.19.0.0/16 | 1 container |
| br-b929ba06e087 | 172.21.0.0/16 | 1 container |
| br-165ba85cf521 | 172.24.0.0/16 | 1 container |
| br-76b57ee77431 | 172.27.0.0/16 | 1 container |

### Serviços Ativos

| Serviço | Porta | Stack | Status |
|---|---|---|---|
| Ollama | 11434 | Nativo | ✅ gemma4:26b · 53 t/s · 2× 1080 Ti |
| ChromaDB | 8000 | Docker | ✅ 8 collections · 384 visual + 105 episodic |
| RAG API | 8500 | Python | ✅ McKee · Field · Block · /search_montagem |
| Visual Search API | 8700 | systemd | ✅ auto_tags · enable-linger |
| memory_manager | 8502 | Python | ✅ |
| Open WebUI | 3000 | Docker | ✅ 14 pipelines |
| n8n | 5678 | Docker | ✅ |
| Nextcloud | 8080 | Docker | ✅ |
| Jellyfin | 8096 | Docker | ✅ |
| Navidrome | 4533 | Docker | ✅ |
| Kiwix | 8888 | Docker | ✅ Wikipedia offline |
| CyberChef | 8100 | Docker | ✅ |
| Syncthing | 22000 | Nativo | ✅ |
| WireGuard | 51820 | Nativo | ✅ 3 peers |
| NPM | 80/443/81 | Docker | ✅ SSL Let's Encrypt |
| SSH | 22 | Nativo | ✅ key-only + fail2ban |
| Open WebUI (root) | 8080 | Docker | ✅ |

### Apps Locais

| App | Path | Uso |
|---|---|---|
| Obsidian | ~/apps/Obsidian-1.12.7.AppImage --no-sandbox | Vault MEMORABILIA |
| Joplin | ~/.config/joplin-desktop/ | 333 notas · histórico completo |
| Firefox | snap | Browser |

### Modelos Ollama

| Modelo | Uso |
|---|---|
| gemma4:26b | Agents 3a/3c/6b/7/8 · 53 t/s |
| llava:7b | Vision fallback |
| nomic-embed-text | Embeddings 768 dims |
| mistral:latest | Tradução · pipelines leves |
| pingpong-story:latest | Custom model |
| pingpong-trailer:latest | Custom model |
| pingpong-3d:latest | Custom model |

---

## Windows PC — 192.168.68.105

### Hardware

| Componente | Spec |
|---|---|
| Motherboard | MSI MAG B660 TOMAHAWK WIFI DDR4 (MS-7D41) |
| GPU | ASUS TUF Gaming RTX 4080 — 16GB VRAM · Ada Lovelace |
| RAM | 64GB DDR4 2133 · 2× 32GB Corsair |
| PSU | Seasonic Vertex GX-1200 · 1200W 80+ Gold |
| Storage C: | Samsung SSD 980 PRO 1TB NVMe — OS + software |
| Storage D: | Samsung SSD 980 PRO 2TB NVMe — active render + projects |
| Storage E: | Seagate Expansion 14.9TB USB HDD — cold archive (shared with Linux BLACKBOX) |
| OS | Windows 11 Pro |

### Role

- Edição: Premiere Pro + CEP MEMORABILIA panel
- Render: RTX 4080
- Vision: qwen3-vl:8b (Ollama 0.6.8)
- Whisper: large-v3

### Shares exportados

| Share | Path Windows | Montado no Linux |
|---|---|---|
| projects | D:\01_PROJECTS | /mnt/win_projects |
| footage_hot | ? | /mnt/win_hot |
| tools | D:\TOOLS | /mnt/win_tools |
| RAG_chromadb | ? | /mnt/win_chromadb |

### Software

| App | Uso |
|---|---|
| Premiere Pro 2026 | Edição + CEP MEMORABILIA |
| After Effects | Motion Graphics (Cenários 2-5) |
| DaVinci Resolve | Color |
| Blender | 3D (Cenário 3) |
| Cinema 4D | 3D (Cenário 3) |
| Obsidian | Vault via Samba \\192.168.68.113\DATA\memorabilia-vault |
| Ollama 0.6.8 | qwen3-vl:8b · ⚠️ NÃO atualizar (bug CUDA #12618) |

---

## Samsung Galaxy — 192.168.68.100

| Item | Detalhe |
|---|---|
| IP local | 192.168.68.100 |
| VPN | 10.0.0.3 (WireGuard — último handshake 6h atrás) |
| Apps | Joplin mobile · Syncthing |
| Uso | Notas em campo · referências visuais |

---

## Roku — offline

| Item | Detalhe |
|---|---|
| Status | Não aparece na rede — provavelmente desligado |
| Uso | Streaming Jellyfin · Navidrome |

---

## HP DeskJet 3755 — 192.168.68.108

| Item | Detalhe |
|---|---|
| IP local | 192.168.68.108 |
| Nome no router | HP6F8240 |
| Connection | Wi-Fi 2.4G |
| Uso | Printer |

---

## iRobot Roomba — 192.168.68.110

| Item | Detalhe |
|---|---|
| IP local | 192.168.68.110 |
| Connection | Wi-Fi 2.4G |
| Uso | Vacuum robô |

---

## TP-Link Deco Mesh

| IP | Nome | Connection | Role |
|---|---|---|---|
| .1 | Router (principal) | Gateway | SSID: XIMBICA |
| .101 | TY_WR | — | Satélite |
| .102 | TY_WR | Wi-Fi 2.4G | Satélite |
| .106 | wlan0 | Wi-Fi 2.4G | Interface wireless |
| .111 | wlan0 | Wi-Fi 2.4G | Interface wireless |

---

## MacBook Pro M1 — Montreal / Field

| Item | Detalhe |
|---|---|
| Chip | Apple M1 — 16GB unified memory |
| Ollama | 7B via Metal · ~20 t/s |
| Role | Human editing · field capture · remote access |
| VPN | ⏳ Pendente — precisa integrar ao WireGuard (10.0.0.4) |
| Status | **NÃO INTEGRADO ao HomeLab** |

---

## Mac Mini M4/M5 — Brazil Unit (a adquirir)

| Item | Detalhe |
|---|---|
| Chip recomendado | Apple M4 Pro · 12-core CPU · 16-core GPU |
| RAM | 24GB unified memory |
| Storage | 512GB SSD |
| Role | Ingest · local Whisper · 1080p proxy · Brazil cluster node |
| VPN | 10.0.0.5 (a configurar) |
| Status | **Aguardar Mac Mini M5 — esperado WWDC Junho 2026** |
| Preço | ~$1,399 CAD |
| Razão espera | 4× faster Neural Engine · 2× faster SSD · Wi-Fi 7 · mesmo preço |

---

## Devices não-HomeLab na rede

| IP | Nome | Device | Nota |
|---|---|---|---|
| .104 | iPhone | iPhone de alguém da casa | Wi-Fi 5G |
| .107 | Galaxy-A54-5G | Celular da casa | Wi-Fi 5G |
| .110 | iRobot | Roomba | Wi-Fi 2.4G |
| .108 | HP6F8240 | HP DeskJet 3755 | Wi-Fi 2.4G |

---

## Cluster Summary

| Machine | Location | GPU | VRAM | RAM | Role | Status |
|---|---|---|---|---|---|---|
| HomeLab Linux | Montreal | 2× GTX 1080 Ti | 22GB | 128GB | AI server · pipeline | ✅ Active · Wired |
| Windows PC | Montreal | RTX 4080 | 16GB | 64GB | Editing · render · vision | ✅ Active · Wi-Fi 5G |
| MacBook Pro M1 | Montreal/field | M1 GPU | 16GB unified | 16GB | Mobile · field | ⏳ Pendente VPN |
| Samsung Galaxy | Montreal/field | — | — | — | Notes · field | ✅ Active · VPN 10.0.0.3 |
| Roku | Montreal | — | — | — | Streaming | ⚠️ Offline |
| Mac Mini M5 | Brazil | M5 Pro GPU | 24GB unified | 24GB | Ingest · Whisper | ❌ A adquirir |

| Métrica | Valor atual | Com Mac Mini |
|---|---|---|
| Total GPUs | 3 (2× NVIDIA + 1× Apple) | 4 |
| Total VRAM | 38GB (22 + 16) | 62GB |
| Total RAM | 208GB (128 + 64 + 16) | 232GB |
| Storage ativo | ~5.2TB NVMe/SSD | ~5.7TB |
| Cold archive | 14.9TB (Seagate shared) | 14.9TB |

---

## Diagrama de rede — SSID: XIMBICA

```
              ┌─────────────────────────┐
              │   TP-Link Deco (mesh)   │
              │   SSID: XIMBICA         │
              │   192.168.68.1          │
              │                         │
              │   Satélites:            │
              │   .101 · .102           │
              └────────────┬────────────┘
                           │
    ┌──────────────────────┼──────────────────────┐
    │ Wired                │ Wi-Fi 5G             │ Wi-Fi 2.4G
    │                      │                      │
┌───┴─────────┐  ┌─────────┴─────────┐  ┌────────┴────────┐
│ HomeLab     │  │ SAMBA .105        │  │ HP6F8240 .108   │
│ .113        │  │ Windows PC        │  │ Printer      │
│ 2× 1080 Ti  │  │ RTX 4080 · 64GB  │  ├─────────────────┤
│ 128GB RAM   │  │ Premiere · CEP    │  │ iRobot .110     │
│ 20 services │  │ Obsidian (Samba)  │  │ Roomba          │
│ Pipeline    │  ├───────────────────┤  ├─────────────────┤
│ Obsidian    │  │ Ximbica .100      │  │ Roku (offline)  │
└──────┬──────┘  │ Samsung Galaxy    │  │ Jellyfin client │
       │         │ VPN 10.0.0.3      │  └─────────────────┘
       │         ├───────────────────┤
       │         │ MacBookPro .103   │
       │         │ M1 · 16GB         │
       │         │ VPN ⏳ pending    │
       │         ├───────────────────┤
       │         │ iPhone .104       │
       │         │ Galaxy-A54 .107   │
       │         │ (não-HomeLab)     │
       │         └───────────────────┘
       │
       │ SMB exports: blackbox · DATA · tutorials
       │ CIFS mounts: win_projects · win_tools · win_hot
       │
       │ WireGuard VPN 10.0.0.0/24
       │  .1 HomeLab (server)
       │  .2 Windows PC
       │  .3 Samsung Galaxy
       │  .4 MacBook M1 ⏳ pending
       │  .5 Mac Mini Brazil ❌ futuro
       │
       └────────── ┌──────────────────┐
                   │ Mac Mini M5      │
                   │ ❌ Brazil · 2026  │
                   │ 24GB unified     │
                   │ ingest · Whisper │
                   └──────────────────┘
```

---

*pingpong · Montreal · April 12, 2026*
*MEMORABILIA · HomeLab Cluster Inventory v1*
