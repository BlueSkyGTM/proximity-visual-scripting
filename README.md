# PROXIMITY-Visual-Scripting (PVS)

A "Sovereign" framework for narrative-driven simulations where the world runs as a **stateless observer**. This repository contains the architectural core for an indie title centered on economic leverage within a high-tension Mars colony lockdown.

> "You didn't know if a game could feel alive without hard-coded triggers. It can."

---

## ## The Game: Mars Colony Lockdown
In this simulation, player progress is not dictated by combat, but by **Economic Arbitrage** and **Systemic Leverage**. You are a contractor navigating a world where every NPC interaction and market shift is a direct reflection of a central, living data source.

### ### The Core Loop
1.  **Acquisition**: Harvest resources (Ore, Energy) or acquire high-value pharmaceuticals.
2.  **Analysis**: Monitor the **Market Engine** for supply/demand signals and trade-route efficiency.
3.  **Execution**: Trade strategically to lower **Colony Stress** or optimize your **Stipend** efficiency.

---

## ## The "Proximity" Framework (The Pull-Model)
PVS abandons traditional "Push-Based" triggers. Instead of scripts forcing updates to the world, the world **pulls** the current state from the **World State Table (WST)**.

### ### How it Works
* **The Source (WST)**: A centralized C# dictionary acting as the "Single Source of Truth" for variables like `ColonyStability` and `MarketInflationRate`.
* **The Transformation**: Visual Scripting graphs (UVS) detect WST changes and recalculate market values or systemic health in real-time.
* **The Presentation**: When you enter an NPC's proximity, the **Narrative API (Yarn Spinner)** pulls the current economic state to determine dialogue tone.
    * *Example*: If `ColonyStress > 70`, a vendor doesn't just swap branches—they dynamically pull "High Tension" strings into their dialogue.

---

## ## Technical Infrastructure
* **Engine**: Unity (2022.3 LTS).
* **Logic (C-Core)**: High-performance math handling supply-demand curves ($Price = BaseValue \times (1 + (Need / Supply))$).
* **Orchestration (UVS)**: Unity Visual Scripting acts as the "Revenue Operating System," automating the "Action Tax" of keeping systems in sync.
* **Narrative**: Yarn Spinner for data-driven, context-dependent dialogue strings.

---

## ## File Map
```text
PROXIMITY-Visual-Scripting/
├── README.md               # The Architectural Manifesto & Game Context
├── GDD.md                  # Master Blueprint — Loop, Mechanics, and Intent
├── CONTEXT.md              # Systemic Event Philosophy — The Pull-Model deep dive
├── CLAUDE.md               # AI Collaboration Protocol — Technical constraints
├── REFERENCES.md           # Economic Standards — The math behind the market
├── tools/
│   ├── visual-scripting.md # UVS Orchestration layer specs
│   └── c-core.md           # High-performance math engine specs
├── agents/
│   └── schemas/            # WST JSON structures and agent matrices
└── orchestration/
    ├── graphs/             # Visual Scripting logic blueprints
    └── dialogue/           # Yarn Spinner Narrative API scripts