# Systemic Event Philosophy: The Pull-Model

## 1. The Logic of Observation
In **PROXIMITY-Visual-Scripting**, we abandon "Push-Based" event triggers. In traditional engines, an action (e.g., a trade) pushes a command to a script. In **PVS**, all actions update the **World State Table (WST)**, and the world—acting as an observer—reevaluates itself.

## 2. Data Orchestration Flow
The system operates in a three-stage cycle that mirrors high-level GTM data enrichment:

1.  **State Update (The Source):** A player action or C-core simulation tick modifies a value in the WST (e.g., `ResourceScarcityIndex` increases).
2.  **Logic Recalculation (The Transformation):** Visual Scripting graphs detect the change. The `MarketSimulationGraph` recalculates `ItemPrices` based on the new scarcity index. 
3.  **Contextual Pull (The Presentation):** When the player enters a "Proximity" zone (an NPC radius or a Terminal), the edge system pulls the current state.
    * *Yarn Spinner:* "Prices are up 20%. The lockdown is squeezing us."
    * *Visual Scripting:* The UI highlights price text in red.

## 3. Benefits of the Pull-Model
- **Decoupling:** Narrative and Economic systems do not need to know about each other; they only need to know about the WST.
- **Scalability:** New NPCs or market items can be added by simply "pointing" them to existing WST variables.
- **Emergent Narrative:** Because logic is based on variable thresholds rather than fixed branches, unique combinations of "Market Stress" and "Player Reputation" create dialogue outcomes that weren't explicitly written, but were *architected*.

## 4. GTM Methodology Alignment
This mirrors a **"Single Source of Truth"** architecture. Just as a Revenue Ops system ensures that Sales, Marketing, and Success all read from the same customer health score, **PVS** ensures that every game system is aligned with the colony's current economic reality.