# Logic Blueprint: WorldStateGraph

## 1. Functional Role
The `WorldStateGraph` is a persistent, global-level Unity Visual Scripting graph. It acts as the **Data Broker** between the C-Core's raw memory and the Unity Engine's game objects.

## 2. Logic Flow & Node Architecture

### A. Initialization (On Start)
1. **Bridge Connection:** Call `C-Core::InitializeStateLedger`.
2. **Data Pull:** Read the initial `world_state_table.json` and populate the runtime Dictionary.
3. **Event Registration:** Subscribe to "Global Tick" events from the C-Core to ensure the graph stays synced.

### B. Read Operations (Getters)
- **Node Type:** Custom Unit `WST_GetVariable`.
- **Inputs:** `String Key` (e.g., "colony_stress_level").
- **Output:** `Object Value` (Auto-cast to Float, Int, or String).
- **Execution:** Zero-latency retrieval from the cached C# Dictionary.

### C. Write Operations (Setters)
- **Node Type:** Custom Unit `WST_SetVariable`.
- **Inputs:** `String Key`, `Object Value`.
- **Logic Gate:** - **Validation:** Check if the value is within the `range` defined in the JSON schema.
    - **Notification:** Trigger a "Value Updated" broadcast event to all **Observers** (e.g., UI, NPCs).
- **Constraint:** Direct writes are only for player-driven events (e.g., `Credits` changes). Market math writes are reserved for the `MarketSimulationGraph`.

## 3. The Observer Pattern
The `WorldStateGraph` implements an observer pattern to minimize "Action Tax." 
- Instead of NPCs polling the WST every frame, the `WorldStateGraph` maintains a list of **Active Observers**.
- When a variable like `ColonyStressLevel` crosses a threshold (e.g., > 50), the graph fires a **State Change Event** only to the systems that care about that threshold.

## 4. Visual Layout Standards
- **Green Groups:** External API Calls (C-Core communication).
- **Blue Groups:** Variable Retrieval logic.
- **Red Groups:** Variable Update logic with safety validation.
- **Yellow Groups:** Event Dispatchers (The "Pull" notifications).

## 5. GTM Methodology Alignment
This graph functions as the **Master Data Management (MDM)** layer of the project. It ensures that regardless of where an action happens (a trade, a dialogue choice, or a random event), the record is centralized and validated before it influences the rest of the ecosystem.