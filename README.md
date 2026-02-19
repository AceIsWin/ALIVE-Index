# ALiVE Mod Indexes — ARMA 3

A community-maintained collection of pre-generated **[ALiVE mod](https://github.com/ALiVEOS/ALiVE.OS)** index files for ARMA 3 terrains. These indexes enable dynamic civilian placement, military placement, and AI commander analysis on community maps.

---

## How to Use an Index

1. Find the folder for your terrain (e.g., `albasrah/`)
2. Copy the **`x/`** folder from that terrain folder into your ARMA 3 mission folder:
   ```
   missions/YourMission.YourTerrain/x/
   ```
3. ALiVE will automatically detect the index when you place an ALiVE module on that map.

> **Archived terrains** (marked 📦 below) still have their index in a `.rar` or `.zip` file inside the folder. Extract the archive first to get the `x/` folder.

---

## Available Terrains

| Folder | Display Name | Status |
|--------|-------------|--------|
| `albasrah` | Al Basrah | ✅ Ready |
| `anizay` | Anizay | 📦 Needs Extraction |
| `avgani_afghan` | Avgani Afghan | ✅ Ready |
| `bala_murghab_afghanistan` | Bala Murghab, Afghanistan | 📦 Needs Extraction |
| `bornholm` | Bornholm | 📦 Needs Extraction |
| `brf_sumava` | BRF Sumava | ✅ Ready |
| `chernarus_2035` | Chernarus 2035 | 📦 Needs Extraction |
| `chernarus_redux` | Chernarus Redux | ✅ Ready |
| `county_leitrim_northern_ireland` | County Leitrim, Northern Ireland | ✅ Ready |
| `dyala_iraq` | Dyala, Iraq | ✅ Ready |
| `esbekistan` | Esbekistan | ✅ Ready |
| `fallujah` | Fallujah | ✅ Ready |
| `fallujah_2` | Fallujah 2.0 | 📦 Needs Extraction |
| `fapovo` | Fapovo | ✅ Ready |
| `farabad` | Farabad | ✅ Ready |
| `farkhar` | Farkhar | ✅ Ready |
| `frl_sbenh` | FRL Sbenh | ✅ Ready |
| `gabreta_csla` | Gabreta — CSLA Iron Curtain | 📦 Needs Extraction |
| `gardez_afghanistan` | Gardez, Afghanistan | ✅ Ready |
| `gc_krayina` | GC Krayina | 📦 Needs Extraction |
| `gm_weferlingen_summer` | Weferlingen Summer (Global Mobilization) | ✅ Ready |
| `gm_weferlingen_winter` | Weferlingen Winter (Global Mobilization) | 📦 Needs Extraction |
| `gos_n_ziwasogo` | GOS N'Ziwasogo | ✅ Ready |
| `green_sea` | Green Sea Terrain | 📦 Needs Extraction |
| `hazarkot` | Hazarkot | ✅ Ready |
| `islapera` | Isla Pera | ✅ Ready |
| `kilopalo5_agora` | Agora | ✅ Ready |
| `korsac` | Korsac | 📦 Needs Extraction |
| `kujari` | Kujari | ✅ Ready |
| `kunduz_cup_frl` | Kunduz — CUP / FRL | ✅ Ready |
| `kunduz_river` | Kunduz River | 📦 Needs Extraction |
| `lingor_3_8` | Lingor 3.8 | ✅ Ready |
| `livonia` | Livonia | 📦 Needs Extraction |
| `lybor` | Lybor | 📦 Needs Extraction |
| `lythium` | Lythium | ✅ Ready |
| `majan` | Majan | ✅ Ready |
| `mandol` | Mandol | 📦 Needs Extraction |
| `mc3_terrain` | MC3 Terrain | ✅ Ready |
| `mogadishu` | Mogadishu | ✅ Ready |
| `namalsk` | Namalsk | 📦 Needs Extraction |
| `napf_winter` | Napf Winter | ✅ Ready |
| `normandy_spearhead_1944` | Normandy — Spearhead 1944 | 📦 Needs Extraction |
| `northern_warzistan_pakistan` | Northern Warzistan, Pakistan | ✅ Ready |
| `opx_mout_town` | OPX MOUT Town | ✅ Ready |
| `reshmaan_province` | Reshmaan Province | ✅ Ready |
| `rosche` | Rosche | ✅ Ready |
| `sa_hatra` | Sa'hatra | 📦 Needs Extraction |
| `sangin_district_helmand_province` | Sangin District, Helmand Province | ✅ Ready |
| `sehreno` | Sehreno | ✅ Ready |
| `sugarlake` | Sugar Lake | ✅ Ready |
| `suursaariv` | Suursaariv | ✅ Ready |
| `swu_france_benouville` | SWU France — Bénouville | 📦 Needs Extraction |
| `tem_anizay` | Anizay (TEM) | ✅ Ready |
| `tem_chernarus` | Chernarus (TEM) | ✅ Ready |
| `tem_chernarusd` | Chernarus — DayZ Edition (TEM) | ✅ Ready |
| `tem_chernarusw` | Chernarus — Winter (TEM) | ✅ Ready |
| `tem_vinjesvingenc` | Vinjesvingenc (TEM) | ✅ Ready |
| `thirsk_winter` | Thirsk Winter | 📦 Needs Extraction |
| `tora_bora` | Tora Bora | ✅ Ready |
| `umb_armavir` | UMB Armavir | ✅ Ready |
| `umb_colombia` | UMB Colombia | ✅ Ready |
| `uzbin` | Uzbin Valley | ✅ Ready |
| `virginia_specwar_facilities` | Virginia SpecWar Facilities | ✅ Ready |
| `western_sahara` | Western Sahara | 📦 Needs Extraction |
| `wgl_palms` | WGL Palms | ✅ Ready |
| `yulakia` | Yulakia | ✅ Ready |
| `zagorsk_khotkovo` | Zagorsk Khotkovo | 📦 Needs Extraction |

**45 ready** · **21 need extraction** · **66 total**

---

## Folder Structure

Each terrain folder follows this layout:

```
<terrain_name>/
├── <terrain_name>.url          # Steam Workshop link (if available)
└── x/
    └── alive/
        └── addons/
            ├── civ_placement/
            │   └── clusters/
            │       └── clusters.<terrain>_civ.sqf
            ├── mil_placement/
            │   └── clusters/
            │       └── clusters.<terrain>_mil.sqf
            ├── fnc_strategic/
            │   └── indexes/
            │       └── objects.<terrain>.sqf
            ├── fnc_analysis/
            │   └── data/
            │       └── data.<terrain>.sqf
            └── main/
                └── static/
                    └── <terrain>_staticData.sqf
```

Archived folders (📦) contain a `.rar` or `.zip` in place of the `x/` folder — extract it to get the same structure.

---

## Contributing a New Index

1. **Fork** this repository and create a feature branch
2. Generate the index using the **in-game ALiVE Map Indexer Module** (see [`.github/copilot-instructions.md`](.github/copilot-instructions.md) for full instructions)
3. Name your terrain folder using **lowercase snake_case** matching the ARMA 3 world classname (e.g., `my_terrain_name/`)
4. Place the generated `x/` folder inside your terrain folder
5. Optionally add a `<terrain_name>.url` file linking to the Steam Workshop page
6. Open a **Pull Request** — include the terrain name and a brief description

### Naming Convention

| Rule | Example |
|------|---------|
| All lowercase | `albasrah` not `AlBasrah` |
| Underscores, no spaces | `tora_bora` not `Tora Bora` |
| No special characters | `gabreta_csla` not `Gabreta - CSLA` |
| No `_Index` suffix | `yulakia` not `Yulakia_Index` |
| Match ARMA 3 world classname where possible | `tem_anizay`, `gm_weferlingen_summer` |

---

## Resources

- [ALiVE Official GitHub](https://github.com/ALiVEOS/ALiVE.OS)
- [ALiVE Wiki — Map Indexing](https://github.com/ALiVEOS/ALiVE.OS/wiki)
- [ARMA 3 SQF Scripting Reference](https://community.bistudio.com/wiki/Category:Scripting_Commands_Arma_3)
- [BIS Community Wiki — Terrain](https://community.bistudio.com/wiki/Arma_3:_Terrains)
