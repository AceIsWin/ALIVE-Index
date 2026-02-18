# Contributing to ALIVE-Index

Thank you for helping expand terrain support for the ALiVE community. This guide covers everything you need to submit a new terrain index or fix an existing one.

---

## What Can I Contribute?

There are two types of accepted contributions:

1. **New terrain indexes** — a complete index for a terrain not yet in this repository
2. **Fixes to existing indexes** — corrections to cluster positions, sizes, or priorities

> **Critical constraint:** Terrain indexes **cannot be hand-coded**. They must be generated using the **ALiVE Map Indexer Module** inside Arma 3. No amount of manual SQF editing can replicate what the indexer produces. If a terrain needs a new index or re-indexing, the full in-game process described below must be followed.

---

## Prerequisites

Before you can generate an index, you need the following set up on your machine:

- **BattlEye disabled** — must be disabled in your Arma 3 launcher or `.cfg` file before indexing
- **Antivirus exclusion** — temporarily disable AV or exclude your Arma 3 indexing folder from scanning (the indexer writes many files rapidly)
- **ALiVE mod installed** in the `@ALiVE` folder (case-sensitive folder name)
  - `ALiVEClient.dll` must be present in `@ALiVE`
  - `alive_object_blacklist.txt` must be present in `@ALiVE`
- **Mikero's Tools** — specifically `deWRP.exe`, which must be accessible via your system `PATH`
- **All `.exe` and `.dll` files unblocked** — right-click → Properties → Unblock in Windows if needed
- **Baretail** (or similar log tail utility) — used to monitor the Arma 3 `.rpt` log file during indexing

---

## Generating a New Terrain Index

### Step 1 — Launch Arma 3

Start Arma 3 with the following mods loaded, replacing `@YourCustomMap` with the actual mod folder:

```
-mod=@ALiVE;@CBA_A3;@YourCustomMap -filePatching
```

### Step 2 — Create the Indexing Mission

1. Open the Arma 3 Editor
2. Place a **player unit**
3. Place the **ALiVE Map Indexer Module** from the ALiVE module list
4. Configure the module:
   - **Object Categorization**: Set to `Yes` for a new terrain (or an existing terrain requiring re-categorization)
   - **Map PBO file path**: Full path to the terrain `.pbo` file (e.g., `@mapname\addons\mapname.pbo`)
   - **Custom Map Bounds**: Leave at `0` by default; if units spawn in the wrong location after indexing, set this to the map size rounded to the nearest 1000
5. Save the mission as `index`

### Step 3 — Start the Indexing Process

1. Launch the mission (Play Scenario)
2. Open the ALiVE interaction menu (default: Right App/Windows Menu key)
3. Select **"Map Indexing"**
4. A `cmd.exe` window will open as `deWRP` processes the terrain
5. When prompted, press the **Up Arrow key** (do NOT press Space or Escape)

### Step 4 — Object Categorization

For each building/object type displayed, select all relevant categories from the list. Use the object's Arma model name as a reference. See the **Object Categorisation Reference** section below for what each category means.

This step only needs to be completed once per terrain (unless the terrain is updated or you want to re-categorize).

### Step 5 — Validate Static Data

Before allowing the indexer to continue to the analysis phase:

1. Navigate to `@ALiVE\indexing\[terrain]\x\alive\addons\main\static\[terrain]_staticData.sqf`
2. Open the file and verify all arrays terminate correctly with `];`
3. Pay particular attention to the `ALIVE_BLACKLIST` array — a missing `];` here will break the entire index
4. Press any key in the Arma 3 window to continue once validated

### Step 6 — Wait for Analysis and Clustering

- The analysis phase takes **10–30 minutes** depending on map size
- Monitor progress using Baretail watching your Arma 3 `.rpt` file
- **Do not close or alt-tab out of Arma 3** — it must remain the active window
- Arma 3 will appear unresponsive during this phase; this is normal
- If the process appears stuck on "Generating Sector Data": copy the `\x` folder from the repository's `scripts\` folder into your mission folder and retry

### Step 7 — Collect the Output

Once complete, all generated index files will be in:

```
@ALiVE\indexing\[terrain]\x\
```

Copy this `x\` folder — that is what gets submitted to this repository.

---

## Object Categorisation Reference

During Step 4, you must assign each object type to one or more categories. ALiVE uses these categories to determine spawning behaviour.

### Building Categories

| Category | Variable | Description |
|---|---|---|
| **Blacklist** | — | Ignore this object (clutter, props, pipes, etc.) |
| **Military (General)** | `ALIVE_militaryBuildingTypes` | Any building found in a military base or camp |
| — Allow Ambient Vehicles | `ALIVE_militaryParkingBuildingTypes` | Vehicles spawn nearby |
| — Allow Ambient Supplies | `ALIVE_militarySupplyBuildingTypes` | Supply crates spawn nearby |
| — Allow HQ | `ALIVE_militaryHQBuildingTypes` | Can be selected as military HQ |
| **Fixed-Wing Aircraft** | `ALIVE_airBuildingTypes` | Runways, hangars, control towers |
| — Military Air | `ALIVE_militaryAirBuildingTypes` | Military airbase structures |
| — Civilian Air | `ALIVE_civilianAirBuildingTypes` | Civilian airport structures |
| **Rotary-Wing Aircraft** | `ALIVE_militaryHeliBuildingTypes` / `ALIVE_civilianHeliBuildingTypes` | Helipads and helicopter zones |
| **Civilian (General)** | `ALIVE_civilianSettlementBuildingTypes` | Residential and commercial buildings |
| — Allow HQ | `ALIVE_civilianHQBuildingTypes` | Can be selected as civilian HQ |
| — Allow Ambient Civilians | `ALIVE_civilianPopulationBuildingTypes` | Ambient civilians spawn here |

### Civilian Infrastructure (High-Priority Targets)

| Type | Variable | Examples |
|---|---|---|
| Power | `ALIVE_civilianPowerBuildingTypes` | Power plant, transformer station |
| Comms | `ALIVE_civilianCommsBuildingTypes` | TV mast, transmitter tower |
| Marine | `ALIVE_civilianMarineBuildingTypes` | Pier, lighthouse, crane |
| Rail | `ALIVE_civilianRailBuildingTypes` | Rail station |
| Fuel | `ALIVE_civilianFuelBuildingTypes` | Gas station, fuel depot |
| Construction | `ALIVE_civilianConstructionBuildingTypes` | Workshops, construction sites |

---

## Testing Your Index

Before submitting, test the index in a mission to confirm it functions correctly.

1. **Create a test mission** in the editor on the target terrain with:
   - A player unit
   - ALiVE Required module
   - ALiVE Virtual AI module (debug enabled, virtualize all except synced)
   - ALiVE Military Objectives module (debug enabled)
   - ALiVE Civilian Objectives module (debug enabled)
2. **Copy the index data** — copy `@ALiVE\indexing\[terrain]\x` into your mission folder:
   `C:\Users\[name]\Documents\Arma 3\missions\IndexTest.[terrain]\x`
3. **Play the scenario** and verify:
   - Mission loads without errors
   - Units spawn in correct locations on the map
   - No SQF errors in the `.rpt` log
4. **Troubleshoot if needed:**
   - Units spawning in the ocean or wrong area → re-index with **Custom Map Bounds** set to the map size (rounded to nearest 1000)
   - Delete all files under `@ALiVE\indexing\[terrain]\x\` **except** `[terrain]_staticData.sqf`, set Object Categorization to `No`, and re-run the indexer

---

## Submitting a New Terrain Index

1. **Fork** this repository
2. **Create a branch** named `terrain/[terrain-folder-name]` (e.g., `terrain/albasrah`)
3. **Add your terrain folder** at the repository root containing:
   - `log.txt` — the log file produced during indexing (found in `@ALiVE\indexing\[terrain]\`)
   - `x/` — the complete generated index folder from `@ALiVE\indexing\[terrain]\x\`
4. **Do not include:**
   - `.url` shortcut files — the repository owner adds these manually
   - `.rar` or `.zip` archives — submit the unzipped `x/` folder only
   - Screenshots or other media
5. **Open a Pull Request** with:
   - **Title**: `Add index: [Terrain Display Name]`
   - **Body**: terrain display name, approximate map size, terrain mod author/source, whether you have tested in-game

---

## Fixing Existing Cluster Data

Acceptable fixes without a full re-index:

- Correcting a cluster center that is offset from the actual settlement
- Adjusting a cluster radius that is too large or too small
- Updating a cluster priority weighting
- Removing a cluster that references non-existent terrain objects

**Do not** manually create new clusters from scratch. If clusters are missing from a terrain, the entire terrain must be re-indexed using the in-game ALiVE Map Indexer Module.

Mark any manual edits with a comment:

```sqf
// MODIFIED: Corrected cluster center — was offset 200m to the north
[_cluster,"center",[1234.5, 5678.9]] call ALIVE_fnc_hashSet;
```

---

## Commit Message Convention

```
add: [terrain] - new index for [Display Name]
fix: [terrain] - [brief description of correction]
docs: [what was updated]
```

Examples:
```
add: albasrah - new index for Al Basrah, Iraq
fix: fallujah - correct cluster c_12 center coordinates
docs: update contributing guide with new step 5 notes
```

---

## Questions

If you are unsure about any part of the process, open a GitHub Issue before starting. Generating an index takes significant time — it is worth clarifying requirements first.
