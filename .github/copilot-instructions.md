# ALiVE Index - Copilot Instructions

## Project Overview

This repository contains terrain index files for the **ALiVE (A.L.I.V.E.)** mod for Arma 3. ALiVE is a framework that creates dynamic, persistent, and immersive mission environments. This project maintains pre-generated index files for multiple Arma 3 terrains to support the ALiVE ecosystem.

### Key Characteristics
- **Language**: SQF (SQFScript) - Arma 3 scripting language
- **Purpose**: Terrain indexing for ALiVE civilian placement, military placement, and strategic analysis
- **Structure**: Multi-terrain repository with standardized addon structure per terrain

---

## Repository Structure

### Directory Layout

```
ALIVE-Index/
├── [terrain-name]/                 # One directory per terrain/map
│   ├── log.txt                     # Processing log from indexing tool
│   ├── [terrain-name].url          # URL file (if available)
│   └── x/
│       └── alive/
│           └── addons/             # ALiVE addon modules
│               ├── civ_placement/   # Civilian placement cluster data
│               ├── mil_placement/   # Military placement cluster data
│               ├── fnc_strategic/   # Strategic analysis data
│               ├── fnc_analysis/    # Function analysis data
│               └── main/            # Main addon data
├── scripts/
│   └── scripts/
│       └── x/
│           └── alive/              # Processing/utility scripts
├── .github/
│   └── copilot-instructions.md      # This file
└── .git/                            # Git repository

```

### Terrain Examples
- `albasrah/` - Al Basrah, Iraq
- `chernarus/`, `chernarusD/`, `chernarusW/` - Chernarus variants
- `fallujah/`, `anizay/`, `farabad/` - Additional Middle East terrains
- `livonia/`, `bornholm/` - European terrains
- And 50+ additional Arma 3 terrains

---

## File Naming Conventions

### Cluster Files
Cluster files follow this naming pattern:
```
clusters.[terrain]_[type].sqf
```

Examples:
- `clusters.albasrah_civ.sqf` - Civilian clusters for Al Basrah
- `clusters.fallujah_mil.sqf` - Military clusters for Fallujah

### Index Files
Generated index files in `fnc_strategic/indexes/`:
```
objects.[terrain].sqf      # Main index file
parsed.objects.[terrain].sqf  # Parsed version
```

### Type Classifications
- `_civ` - Civilian placement clusters
- `_mil` - Military placement clusters
- `_air` - Airfield clusters (implicit in strategic)

---

## SQF Code Conventions

### Cluster Structure
Cluster files use a standardized data structure:

```sqf
#include "\x\alive\addons\civ_placement\script_component.hpp"
ALIVE_clustersCiv = [] call ALIVE_fnc_hashCreate;

_cluster = [nil, "create"] call ALIVE_fnc_cluster;
_nodes = [];

// Add node data
_nodes set [count _nodes, ["nodeID", [x, y, z]]];

// Set cluster properties
[_cluster,"nodes",_nodes] call ALIVE_fnc_hashSet;
[_cluster,"clusterID","c_0"] call ALIVE_fnc_hashSet;
[_cluster,"center",[centerX, centerY]] call ALIVE_fnc_hashSet;
[_cluster,"size",radius] call ALIVE_fnc_hashSet;
[_cluster,"type","CIV"] call ALIVE_fnc_hashSet;
[_cluster,"priority",50] call ALIVE_fnc_hashSet;
[_cluster,"debugColor","ColorBlack"] call ALIVE_fnc_hashSet;

// Register cluster
[ALIVE_clustersCiv,"c_0",_cluster] call ALIVE_fnc_hashSet;
```

### Key Properties

| Property | Type | Description | Example |
|----------|------|-------------|---------|
| `clusterID` | String | Unique cluster identifier | `"c_0"`, `"c_1"` |
| `nodes` | Array | Array of [nodeID, [x, y, z]] positions | `["105722", [1548.55, 566.505, 1.08]]` |
| `center` | Array | [x, y] center coordinates | `[1607.34, 583.078]` |
| `size` | Number | Cluster radius in meters | `150`, `255.39` |
| `type` | String | Cluster type: `"CIV"`, `"MIL"`, `"AIR"` | `"CIV"` |
| `priority` | Number | Priority weight (0-100) | `50`, `100` |
| `debugColor` | String | Color for debug display | `"ColorBlack"`, `"ColorRed"` |

### Positioning Conventions
- **Coordinates**: Use [x, y, z] format (world coordinates)
- **Z-values**: Include elevation; use 0 or terrain elevation
- **Precision**: Maintain decimal places for accuracy (typically 2-5 decimals)

---

## Processing Workflow

### Log Files
Each terrain directory contains a `log.txt` file generated during indexing. Example log flow:
1. **Start**: `Starting Map Index for [terrain] on [date]`
2. **Path Setup**: Maps paths to Arma installation and output locations
3. **deWrp Analysis**: Uses DeWrp tool to extract terrain model data
4. **Filtering**: Ignores irrelevant objects (vegetation, small items, etc.)
5. **Indexing**: Generates cluster data and indexes
6. **Output**: Writes `.sqf` cluster files and parsed indexes

### Log Markers
- `>>>>>>>>>>` - Section headers
- `----- Ignoring :` - Filtered object types
- `Copying` - File write operations
- Processing status lines with timestamps

---

## Map Indexing Process (Manual Generation)

### Prerequisites for Generating New Indexes

Before indexing a map, ensure:
- **BattlEye MUST BE DISABLED** (via A3 Launcher or .cfg file)
- Temporarily disable AV software or exclude indexing folder from scanning
- ALiVE in `@ALiVE` folder (case-sensitive)
- `ALiVEClient.dll` and `alive_object_blacklist.txt` in `@ALiVE` folder
- Mikero's Tools (deWRP.exe) installed and accessible via PATH
- All .exe and .dll files unblocked in Windows Properties
- Baretail installed to monitor RPT file during indexing

### Step-by-Step Indexing Instructions

1. **Launch Arma 3 with Command Line**
   ```
   -mod=@ALiVE; @CBA_A3; @YourCustomMap -filePatching
   ```

2. **Create Indexing Mission**
   - Open Editor
   - Place a player unit
   - Place the ALiVE Map Indexer Module
   - Configure Module Settings:
     - **Object Categorization**: Select "Yes" for new maps or existing maps requiring updates
     - **Map PBO file path**: Full path to terrain PBO (e.g., `@mapname\addons\mapname.pbo`)
     - **Custom Map Bounds**: Set to 0 by default; use map size rounded to nearest 1000 if needed
   - Save mission as `index`

3. **Start Indexing Process**
   - Launch game and go to map screen
   - Open ALiVE interaction menu (Right App Menu by default)
   - Select "Map Indexing"
   - A `cmd.exe` window launches (deWRP processing)
   - **Press UP arrow** when prompted (NOT Space or ESC)

4. **Object Categorization**
   - For each displayed object, select all relevant categories
   - Use the object's Arma model name as reference
   - Follow Static Data category guidelines (see below)

5. **Static Data Validation**
   - After categorization completes, pause before final indexing
   - Edit `@ALiVE\indexing\mapname\x\alive\addons\main\static\mapname_staticData.sqf`
   - **Critical**: Verify all arrays terminate with `];` (especially `ALIVE_BLACKLIST`)
   - Press any key to continue

6. **Analysis & Clustering**
   - Process takes 10-30 minutes depending on map size
   - Monitor progress in Baretail (RPT file)
   - **DO NOT CLOSE Arma 3** - must remain active window
   - Arma 3 will be unresponsive; this is normal
   - If stuck on "Generating Sector Data": copy `\x` folder from `\scripts` folder into mission folder

7. **Completion**
   - All indexed files created in `@ALiVE\indexing\mapname\x`
   - Ready for testing and distribution

### Static Object Data Categories

ALiVE requires human classification of map objects as Civilian or Military before generating clusters. Objects context varies by map designer intent. **Each building type must be configured with specific properties** that control how the Military and Civilian Placement modules use those buildings.

#### Category Definitions

| Category | Array Variable | Description | Properties |
|----------|---|---|---|
| **Blacklist** | N/A | Objects to remove (clutter, carts, pipes, etc) | No placement impact |
| **Military Buildings (General)** | `ALIVE_militaryBuildingTypes` | Any building in military base/camp | **Critical** for military objectives |
| ├─ Allow Ambient Vehicles | `ALIVE_militaryParkingBuildingTypes` | Vehicles spawn nearby | Mil Placement spawns vehicles around these buildings |
| ├─ Allow Ambient Supplies | `ALIVE_militarySupplyBuildingTypes` | Supply boxes spawn nearby | Mil Placement spawns supply boxes around these buildings |
| └─ Allow HQ | `ALIVE_militaryHQBuildingTypes` | Can be selected as HQ | Mil Placement selects HQ location from this list |
| **Aircraft (Fixed Wing)** | `ALIVE_airBuildingTypes` | Runways, hangars, towers | Can be military or civilian (classify separately) |
| ├─ Military | `ALIVE_militaryAirBuildingTypes` | Military airbase structures | e.g., military control tower |
| └─ Civilian | `ALIVE_civilianAirBuildingTypes` | Civilian airport structures | e.g., civilian hangar |
| **Aircraft (Rotary Wing)** | `ALIVE_militaryHeliBuildingTypes`, `ALIVE_civilianHeliBuildingTypes` | Helipads and heli zones | Specify military or civilian separately |
| **Civilian Buildings (General)** | `ALIVE_civilianSettlementBuildingTypes` | Any residential building | **Critical** for civilian objectives |
| ├─ Allow HQ | `ALIVE_civilianHQBuildingTypes` | Can be Mil Placement HQ | Can be selected as civilian HQ |
| └─ Allow Ambient Civilians | `ALIVE_civilianPopulationBuildingTypes` | Civs spawn here | Civ Pop module spawns ambient civilians in/around these buildings |
| **Civilian Infrastructure** | See infrastructure types below | Priority targets for tasks | Used for high-priority objective generation |

#### Infrastructure Categories (Civilian Priority Targets)

| Type | Array Variable | Example |
|------|---|---|
| Power | `ALIVE_civilianPowerBuildingTypes` | Power plant, transformer station |
| Comms | `ALIVE_civilianCommsBuildingTypes` | TV mast, transmitter tower |
| Marine | `ALIVE_civilianMarineBuildingTypes` | Pier, lighthouse, crane |
| Rail | `ALIVE_civilianRailBuildingTypes` | Rail station, tracks |
| Fuel | `ALIVE_civilianFuelBuildingTypes` | Gas station, fuel depot |
| Construction | `ALIVE_civilianConstructionBuildingTypes` | Work-in-progress sites, workshops |

### Static Data File Format

Static data arrays use partial object name matching. For example:
- `"house_"` matches `house_1`, `house_2`, `house_2a`, etc.
- `"bunker"` matches any variant containing "bunker" in the name

```sqf
// Military buildings that allow vehicle parking
ALIVE_militaryParkingBuildingTypes = ALIVE_militaryParkingBuildingTypes + [
	"bunker",
	"barrack",
	"mil_house",
	"mil_controltower",
	"deerstand"
];

// Civilian houses and shops for population placement
ALIVE_civilianPopulationBuildingTypes = ALIVE_civilianPopulationBuildingTypes + [
	"house_",
	"shop_",
	"garage_"
];

// Infrastructure targets
ALIVE_civilianPowerBuildingTypes = ALIVE_civilianPowerBuildingTypes + [
	"powerstation",
	"trafostanica"
];

ALIVE_civilianCommsBuildingTypes = ALIVE_civilianCommsBuildingTypes + [
	"transmitter_tower",
	"telek"
];
```

### Testing the Generated Index

1. **Create Test Mission**
   - Create new mission in editor
   - Place player unit
   - Place ALiVE Required module
   - Place ALiVE Virtual AI module (enable debug, virtualize all except synced)
   - Place ALiVE Mil. Obj. module (enable debug)
   - Place ALiVE Civ. Obj. module (enable debug)
   - Save as `IndexTest`

2. **Copy Index Data**
   - Copy `@ALiVE\indexing\mapname\x` folder to mission folder
   - Example: `C:\My Documents\Arma 3\missions\IndexTest.YourMap\x`
   - Verify `yourmap_staticData.sqf` exists in `x\alive\addons\main\static\`

3. **Validate Index**
   - Press Play Scenario
   - Check mission loads without errors
   - Verify units spawn in correct locations
   - Monitor RPT for any warnings

4. **Troubleshooting Index Issues**
   - If spawning in wrong locations:
     - Re-index map with Custom Map Bounds set to map size rounded to nearest 1000
     - Delete all files under `@ALiVE\indexing\mapname\x\` **EXCEPT** `mapname_staticData.sqf`
     - Edit static data to correct `ALIVE_MapBounds` value
     - Re-run indexer with Object Categorization set to "No"

---

## Development Guidelines for AI Agents

### CRITICAL: Index Generation Cannot Be Manual

**Indexes MUST be generated using the in-game ALiVE Map Indexer Module.** There is no method to manually create indexes from scratch. All cluster data in this repository was generated through the automated indexing process described above. Manual hand-coding of indexes is not supported and will not function correctly with ALiVE.

### When Modifying Existing Terrain Index Data

Modifications to existing indexes should be limited to:
- Bug fixes in node positions or cluster boundaries
- Corrections to cluster properties (size, priority, etc.)
- Addition of missing clusters identified during testing
- Documentation and comment improvements

**DO NOT manually create new clusters from scratch.** If a terrain needs re-indexing or cluster updates:
1. The entire terrain must be re-indexed using the in-game ALiVE Map Indexer Module
2. Follow the complete Step-by-Step Indexing Instructions above
3. Use existing `mapname_staticData.sqf` files to maintain consistency

### When Modifying Existing Clusters

1. **Understand the Terrain Structure**
   - Each terrain uses the same addon structure
   - Cluster IDs must be unique within terrain (`c_0`, `c_1`, `c_2`, etc.)
   - Nodes reference actual terrain objects by ID

2. **Maintain Consistency**
   - Follow exact naming conventions for files and cluster IDs
   - Keep cluster properties in the documented order
   - Preserve the `#include` statements at file start
   - Use consistent formatting for `_nodes set` operations

3. **Data Integrity**
   - Verify coordinates are realistic for the terrain
   - Ensure `size` values match cluster distribution
   - Maintain sequential cluster numbering
   - Keep debug colors consistent (typically `"ColorBlack"`)
   - Verify node IDs correspond to actual terrain objects

4. **Comment Guidelines**
   - Include section comments for terrain regions
   - Mark changes with `// MODIFIED:` when updating
   - Reference cluster ID in comments: `// Cluster c_0: Downtown area`
   - Document why changes were made

5. **Testing Approach**
   - Validate SQF syntax before committing
   - Check that node positions fall within cluster boundaries
   - Verify cluster counts match terrain file comments
   - Ensure no duplicate cluster IDs across files
   - Test in-game to ensure clusters function correctly

### Common Modification Tasks

**Correcting Cluster Center Coordinates:**
```sqf
// If cluster center is offset, update it
[_cluster,"center",[correctedX, correctedY]] call ALIVE_fnc_hashSet;
```

**Adjusting Cluster Size/Radius:**
```sqf
// If cluster radius needs correction
[_cluster,"size",newRadius] call ALIVE_fnc_hashSet;
```

**Updating Cluster Priority:**
```sqf
// Adjust priority weighting (0-100)
[_cluster,"priority",newPriority] call ALIVE_fnc_hashSet;
```

**Removing Invalid Nodes:**
```sqf
// Reconstruct _nodes array without the invalid node
_nodes = [];
_nodes set [count _nodes, ["valid_node_1", [x, y, z]]];
_nodes set [count _nodes, ["valid_node_2", [x, y, z]]];
// ... skip the invalid node ...
[_cluster,"nodes",_nodes] call ALIVE_fnc_hashSet;
```

**NOTE:** Do NOT manually add entirely new clusters. Use the in-game ALiVE Map Indexer Module if clusters are missing or need to be regenerated.

---

## Integration Points

### ALiVE Framework Connection
- Terrain indexes feed into ALiVE's civilian and military placement systems
- The `fnc_strategic` addon enables tactical analysis for AI commanders
- Cluster data controls spawn locations for dynamic units

### Arma 3 Mod Integration
- Uses Arma 3 function library patterns
- Compatible with ALiVE versions supporting the indexed terrains
- Requires proper PBO structure in ALiVE mod directory

### Processing Pipeline
- **Input**: Arma 3 terrain PBO files (`.pbo`)
- **Processing**: External deWrp tool extracts and analyzes models
- **Output**: Pre-generated SQF cluster and index files
- **Distribution**: Committed to this repository for version control

---

## Common Patterns & Best Practices

### Pattern: Hash-Based Data Structure
```sqf
// ALiVE uses hash maps (associative arrays) extensively
ALIVE_clustersCiv = [] call ALIVE_fnc_hashCreate;  // Create empty hash
[_cluster,"key",value] call ALIVE_fnc_hashSet;     // Set value
_value = [_cluster,"key"] call ALIVE_fnc_hashGet;  // Get value
```

### Pattern: Array-Based Node Lists
```sqf
_nodes = [];
_nodes set [count _nodes, element];  // Append to array
```

### Pattern: State Initialization
```sqf
[_cluster, "state", _cluster] call ALIVE_fnc_cluster;  // Initialize cluster state
```

### Best Practice: Include Guards
Always include the necessary script components at file start:
```sqf
#include "\x\alive\addons\civ_placement\script_component.hpp"
```

---

## Troubleshooting & Support

### Common Issues

**Issue**: Clusters not appearing in ALiVE
- **Check**: Verify cluster IDs are unique within the file
- **Check**: Ensure node positions are valid (not NaN or extreme values)
- **Check**: Confirm cluster type matches the file name convention

**Issue**: SQF syntax errors
- **Check**: Verify brackets are balanced
- **Check**: Ensure semicolons end each statement
- **Check**: Validate hash function calls use correct syntax

**Issue**: Coordinate issues
- **Check**: Verify z-coordinates reflect terrain elevation
- **Check**: Ensure x,y are within terrain boundaries
- **Check**: Check for coordinate precision issues (rounding errors)

### References
- Arma 3 SQF Documentation: https://community.bistudio.com/wiki/Category:Scripting_Commands_Arma_3
- ALiVE Official GitHub: https://github.com/ALiVEOS/ALiVE.OS
- ALiVE Wiki: https://github.com/ALiVEOS/ALiVE.OS/wiki

---

## File Modification Checklist

When making changes to terrain index files:

- [ ] Verified cluster IDs are unique in the file
- [ ] Checked node positions are within expected terrain bounds
- [ ] Confirmed SQF syntax is valid (brackets, semicolons)
- [ ] Updated comments to reflect changes
- [ ] Tested in ALiVE if possible
- [ ] Committed with descriptive message mentioning terrain and change type
- [ ] Updated any related documentation

---

## Version Control Notes

- **Commit Messages**: Include terrain name and cluster count changes
  - Example: `update: albasrah - add 5 new civilian clusters in downtown area`
- **Line Endings**: Use LF (Unix style) for consistency
- **File Encoding**: UTF-8 without BOM
- **Branching**: Create feature branches for new terrain indexes

---

**Last Updated**: 2026-01-31  
**Applies To**: ALiVE Index Repository v1.0+
