# Game Design Document: PROXIMITY-Visual-Scripting

## 1. Core Loop: The Arbitrage
The player is a contractor within a high-tension Mars colony lockdown. Survival and progress are not dictated by combat, but by **Economic Leverage**.

- **Phase A (Acquisition):** Harvest resources (Ore, Energy) or acquire tradeable goods (Pharmaceuticals) through systemic interactions.
- **Phase B (Analysis):** Monitor the **Market Engine** for supply/demand signals and trade-route efficiency shifts.
- **Phase C (Execution):** Execute trades or utilize resources to lower **Colony Stress** or increase **Stipend** efficiency.

## 2. Technical Infrastructure
### A. The World State Table (WST)
A centralized C#-based dictionary that serves as the Source of Truth. All other systems "pull" from this table.
- **Key Variables:** `ColonyStability`, `MarketInflationRate`, `PlayerReputation`, `ResourceScarcityIndex`.

### B. Unity Visual Scripting (UVS)
The primary orchestration medium. UVS is used to:
- Map the flow of logic between the WST and the Game World.
- Handle "Action Tax" automation (e.g., automatically adjusting prices based on player inventory volume).

### C. Yarn Spinner (Narrative API)
Yarn Spinner does not store dialogue trees; it queries the WST. 
- NPCs behave as **State-Based Observers**.
- *Example:* A Vendor NPC doesn't have a "mean" branch. They pull the `ColonyStress` variable; if it is > 70, their dialogue dynamically shifts to a "High Tension" tone.

## 3. Tooling & Pipeline
- **Engine:** Unity (2022.3 LTS or newer).
- **Logic:** Unity Visual Scripting + C Core.
- **Narrative:** Yarn Spinner for context-dependent strings.
- **Inspiration:** *Disco Elysium* (Systemic dialogue), *Citizen Sleeper* (Resource-based survival).

## 4. GTM Alignment
This GDD serves as a technical spec for a **Responsive Operating System**. The mechanics are designed to demonstrate how a central data source can drive complex, automated responses in edge environments (NPCs/Markets).