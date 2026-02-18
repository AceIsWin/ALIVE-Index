# ALIVE-Index

> Pre-generated terrain index files for the [ALiVE mod](https://github.com/ALiVEOS/ALiVE.OS) for Arma 3, covering **67 community terrains**.

---

## What is ALiVE?

**ALiVE (A.L.I.V.E.)** is an Arma 3 mod that transforms the editor into a system for fully dynamic, persistent, and intelligent missions. It provides AI commanders that manage entire battlefields, civilian population modules that bring maps to life, and an operations layer that persists between sessions.

To do all of this, ALiVE needs to know where the buildings, roads, military installations, and civilian settlements are on each terrain — that information is stored in a **terrain index**.

- ALiVE on GitHub: [ALiVEOS/ALiVE.OS](https://github.com/ALiVEOS/ALiVE.OS)
- ALiVE Wiki: [ALiVE.OS Wiki](https://github.com/ALiVEOS/ALiVE.OS/wiki)

---

## What This Repository Provides

Generating a terrain index requires running the **ALiVE Map Indexer Module** inside a live Arma 3 session — a process that takes 10–30 minutes per terrain and requires specific tools (Mikero's deWrp, BattlEye disabled, custom launch flags). Most mission makers should not need to do this themselves.

This repository provides **ready-to-use pre-generated index files** for 67 community terrains, so you can drop them straight into your mission and start building.

Each terrain folder contains:

- **`x/alive/addons/`** — the index data (civilian clusters, military clusters, strategic analysis)
- **`log.txt`** — the output log from the indexing session
- **`[name].url`** — a shortcut to the terrain's Steam Workshop page (where available)

---

## How to Use These Indexes

### 1. Find your terrain

Look up your terrain in the [Supported Terrains](#supported-terrains) table below. Note its **folder name**.

### 2. Get the index files

Clone or download this repository, then navigate to the terrain folder. The data you need is inside the `x/` subfolder:

```
ALIVE-Index/
└── albasrah/
    └── x/          <-- this is what you need
        └── alive/
            └── addons/
                ├── civ_placement/    (civilian placement data)
                ├── mil_placement/    (military placement data)
                ├── fnc_strategic/    (strategic analysis data)
                ├── fnc_analysis/     (function analysis data)
                └── main/             (core addon data)
```

> **Note:** A small number of terrain folders currently contain only a `.rar` archive rather than an extracted `x/` folder. Extract the archive to access the index files.

### 3. Copy into your mission

Copy the **entire `x/` folder** into your Arma 3 mission folder, alongside your `mission.sqm`:

```
Documents\Arma 3\missions\YourMission.YourTerrain\
├── mission.sqm
└── x\                   <-- paste the x/ folder here
    └── alive\
        └── addons\
            └── ...
```

### 4. Set up ALiVE in the editor

ALiVE will automatically detect and use the index. Place the standard ALiVE modules in your mission:

- **ALiVE Required** module (mandatory)
- **ALiVE Military Objectives** — for dynamic military operations
- **ALiVE Civilian Objectives** — for civilian population

Refer to the [ALiVE Wiki](https://github.com/ALiVEOS/ALiVE.OS/wiki) for full mission setup instructions.

---

## Supported Terrains

Steam Workshop links marked **—** will be added as they become available. The `[R]` suffix on terrain names denotes a community **Remastered** or **Redux** variant of an older map.

### Middle East / Afghanistan / Central Asia

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `albasrah` | Al Basrah, Iraq | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2783637290) |
| `Anizay` | Anizay | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1537973181) |
| `tem_anizay` | Anizay (TEM variant) | — |
| `Avgani Afghan` | Avgani Afghan | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1320658317) |
| `Bala Murghab, Afghanistan` | Bala Murghab, Afghanistan | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2781043850) |
| `Dyala Iraq` | Dyala, Iraq | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=680808574) |
| `Esbekistan` | Esbekistan | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=815171749) |
| `Fallujah 2.0` | Fallujah 2.0 | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2926828901) |
| `fallujah` | Fallujah (original) | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=908733096) |
| `Farkhar` | Farkhar Valley, Afghanistan | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1281275340) |
| `farabad` | Farabad | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2917444360) |
| `frl_sbenh` | FRL Sbeneh | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1644071854) |
| `gardez_afghanistan` | Gardez, Afghanistan | — |
| `HazarKot` | Hazar-Kot Valley | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=766294759) |
| `Kujari` | Kujari | — |
| `Kunduz  CUP - FRL` | Kunduz (CUP / FRL) | — |
| `Kunduz River` | Kunduz River | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3078351739) |
| `lythium` | Lythium | — |
| `majan` | Majan | — |
| `Mandol Dev Version` | Mandol | [Steam](https://steamcommunity.com/workshop/filedetails/?id=2537308551) |
| `Northern Warzistan, Pakistan` | Northern Warzistan, Pakistan | — |
| `Reshmaan Province` | Reshmaan Province | — |
| `Sa_hatra` | Sa'hatra, Iraq | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3019928771) |
| `sangin_distirict_helmand_province` | Sangin District, Helmand Province | — |
| `Tora Bora` | Tora Bora, Afghanistan | — |
| `uzbin` | Uzbin Valley, Afghanistan | — |

### Africa

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `fapovo` | Fapovo | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1910457930) |
| `GOS N_Ziwasogo` | GOS N'Ziwasogo | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=694603075) |
| `kilopalo5_agora` | Agora | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1932646884) |
| `Mogadishu` | Mogadishu, Somalia | — |
| `Western Sahara` | Western Sahara | — |

### Eastern Europe / Russia

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `Chernarus 2035` | Chernarus 2035 | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1113631358) |
| `ChernarusRedux_Index` | Chernarus Redux | — |
| `gc_krayina_Index` | Krayina, Ukraine | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3141327661) |
| `Green Sea Terrain` | Green Sea Terrain | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2645015212) |
| `Korsac` | Korsac | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3043043427) |
| `Namalsk [R]` | Namalsk \[R\] | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3013966707) |
| `tem_chernarus` | Chernarus (TEM) | — |
| `tem_chernarusd` | Chernarus Desert (TEM) | — |
| `tem_chernarusw` | Chernarus Winter (TEM) | — |
| `umb_armavir` | Armavir | — |
| `Zagorsk Khotkovo` | Zagorsk Khotkovo | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3129318257) |

### Central / Northern Europe

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `Bornholm [R]` | Bornholm \[R\] | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2914536900) |
| `brf_sumava` | Sumava | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2947655994) |
| `Gabreta - CSLA Iron Curtain` | Gabreta (CSLA Iron Curtain) | — |
| `gm_weferlingen_summer` | Weferlingen Summer (Global Mobilization) | — |
| `Lybor` | Lybor | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3013515917) |
| `NapfWinterindex` | Napf Winter | — |
| `Rosche` | Rosche, Germany | — |
| `Suursaariv` | Suursaari Island | — |
| `Thirsk Winter [R]` | Thirsk Winter \[R\] | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=3008157411) |
| `Weferlingen - Global Mobilization` | Weferlingen (Global Mobilization) | — |
| `Yulakia_Index` | Yulakia | — |

### Western Europe

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `County_Leitrim_Northern_Ireland` | County Leitrim, Northern Ireland | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=1679759270) |
| `Livonia` | Livonia | — |
| `Normandy - Spearhead 1944` | Normandy — Spearhead 1944 | — |
| `sehreno` | Sehreno | — |
| `swu_france_benouville_Index` | France — Benouville | — |
| `tem_vinjesvingenc` | Vinjesvingen (TEM) | — |

### Americas / Tropical / Island

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `islapera` | Isla Pera | [Steam](https://steamcommunity.com/sharedfiles/filedetails/?id=2917444360) |
| `Lingor_3_8` | Lingor Island | — |
| `mc3_terrain` | MC3 Terrain | — |
| `sugarlake` | Sugar Lake | — |
| `umb_colombia` | Colombia | — |
| `virginia_specwar_facilities` | Virginia SpecWar Facilities | — |
| `wgl_palms` | WGL Palms | — |

### Fictional / MOUT / Training

| Folder | Terrain | Steam Workshop |
|---|---|:---:|
| `OPX MOUT Town` | OPX MOUT Town | — |

---

## Repository Structure

```
ALIVE-Index/
├── [terrain-folder]/          # One directory per terrain (67 total)
│   ├── log.txt                # Output log from the indexing session
│   ├── [name].url             # Steam Workshop shortcut (where available)
│   └── x/
│       └── alive/
│           └── addons/        # Index data — do NOT edit these files manually
│               ├── civ_placement/
│               ├── mil_placement/
│               ├── fnc_strategic/
│               ├── fnc_analysis/
│               └── main/
├── scripts/                   # Internal processing scripts used by the ALiVE Map Indexer
│                              # (not needed by mission makers)
└── .github/
    └── copilot-instructions.md
```

> The `scripts/` folder contains the FSM and SQF files that power the in-game ALiVE Map Indexer. Mission makers do not need these — they are for contributors generating new indexes.

---

## Contributing

Want to add a terrain that isn't listed here, or fix incorrect cluster placement on an existing one?

See [CONTRIBUTING.md](CONTRIBUTING.md) for full instructions including prerequisites, the step-by-step indexing process, object categorisation guidance, and how to submit a pull request.

**Branch naming:** `terrain/[folder-name]` (e.g., `terrain/albasrah`)

**Important:** Terrain indexes cannot be hand-coded. They must be generated using the ALiVE Map Indexer Module inside a live Arma 3 session.

---

## Links

| Resource | Link |
|---|---|
| ALiVE mod (GitHub) | [ALiVEOS/ALiVE.OS](https://github.com/ALiVEOS/ALiVE.OS) |
| ALiVE Wiki | [ALiVE.OS Wiki](https://github.com/ALiVEOS/ALiVE.OS/wiki) |
| Arma 3 SQF reference | [community.bistudio.com](https://community.bistudio.com/wiki/Category:Scripting_Commands_Arma_3) |
| Bohemia Interactive Community | [community.bistudio.com](https://community.bistudio.com/wiki/Main_Page) |
