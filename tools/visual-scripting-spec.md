# Technical Specification: Unity Visual Scripting Architecture

## 1. The Orchestration Mandate
Unity Visual Scripting is the primary medium for **PVS**. It is responsible for monitoring the **World State Table (WST)** and executing logic transformations that drive the UI, NPC behavior, and Market fluctuations.

## 2. Core Graph Architecture
The system is divided into four primary specialized graphs to ensure modularity and high-speed debugging:

### A. `WorldStateGraph` (The Source)
- **Role:** Data Controller.
- **Function:** Standardizes Read/Write operations to the WST.
- **Nodes:** Custom "Get Variable" and "Set Variable" nodes mapped to C# Dictionary keys.
- **Priority:** Must execute first in the frame-order to ensure all dependent systems read fresh data.

### B. `MarketSimulationGraph` (The Engine)
- **Role:** Economic Processor.
- **Input:** `ResourceScarcityIndex`, `PlayerInventoryVolume`, `TradeRouteEfficiency`.
- **Transformation:** Implements the Supply-Demand curve logic defined in `references.md`.
- **Output:** Updates `ItemPrices` and `MarketStability` variables.

### C. `ContextualTriggerGraph` (The Observer)
- **Role:** State Evaluator.
- **Logic:** Compares WST variables against "Five Archetype" thresholds (e.g., *IF ColonyStress > 80 AND Stability < 30 THEN State = Desperation*).
- **Function:** Passes the translated "Human State" to the Yarn Spinner API.

### D. `ActionAutomationGraph` (The Optimizer)
- **Role:** "Action Tax" Reducer.
- **Function:** Automates redundant tasks such as inventory weight calculations, stipend distribution, and UI color-state updates (e.g., turning price text red if inflation is > 10%).

## 3. Node Standards & Optimization
- **No Tight Loops:** Visual scripts must be event-driven or gated by "On Value Changed" observers to prevent CPU spiking.
- **Data Encapsulation:** Logic nodes must not hold local state. They must pull from the WST, process, and write back immediately.
- **Visual Clarity:** All graphs must use color-coded groups (e.g., Green for Economic Input, Purple for Narrative Output).

## 4. Integration with C-Core
Complex floating-point math (e.g., exponential decay of trade-route efficiency) is handled in **C/C++** and exposed to UVS as custom nodes. This ensures the "Heavy Lifting" is high-performance while the "Orchestration" remains visual and iterative.