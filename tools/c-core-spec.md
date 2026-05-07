# Technical Specification: C-Core Engine Architecture

## 1. The Sovereign Mandate
The C-Core is responsible for the **Mathematical Integrity** of the simulation. By offloading complex calculations to a low-level implementation, we ensure the "Action Tax" on the CPU is minimized, allowing for high-fidelity agent simulations and market-clearing logic that standard high-level scripts cannot sustain.

## 2. Core Functional Modules

### A. `StateLedger.c` (Memory Management)
- **Role:** The back-end for the World State Table (WST).
- **Architecture:** A packed struct or a contiguous memory block (heap-allocated) to minimize cache misses.
- **Data Persistence:** Handles the serialization and deserialization of the global state for "Safe-Sovereign" save states.

### B. `MarketClearing.c` (High-Frequency Math)
- **Role:** Executes the Supply-Demand algorithms defined in `references.md`.
- **Logic:** Uses floating-point math to calculate `PriceFluctuation` based on:
  - `GlobalInventoryVolume`
  - `MarketStressVelocity` (how fast prices change in response to player action)
  - `DecayFunctions` (how prices stabilize over time).

### C. `AgentOrchestrator.c` (The Brain)
- **Role:** Manages the "Internal State" of the five NPC archetypes.
- **Function:** Processes raw data from the WST and transforms it into the "Human State" (Prosperity, Desperation, etc.) before passing the pointer to the Visual Scripting layer.

## 3. The Bridge: Interop with Unity
The C-Core is integrated into Unity via **P/Invoke** or as a **Native Plugin**.
- **The "Pull" Protocol:** Unity Visual Scripting (UVS) calls specific entry points in the C library to retrieve calculated values.
- **Safety:** The C-Core is "Read-Heavy." The UVS layer can only "Write" through strict, validated setter functions to prevent state corruption.

## 4. GTM Methodology Alignment
This architecture demonstrates **Modular Scalability**. By isolating the business logic (the Market) from the presentation layer (Unity), we create a system that can be audited, stress-tested, and optimized independently—mirroring the design of high-performance revenue data engines.