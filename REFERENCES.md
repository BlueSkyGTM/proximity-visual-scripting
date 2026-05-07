# Logic & Economic Standards: PROXIMITY-Visual-Scripting

## 1. Economic Emulation Models
To ensure a "Fair Market" that reacts to data rather than scripts, the following models are prioritized:

### A. Dynamic Supply-Demand Curves
- **Logic:** Price is a function of `ResourceScarcityIndex` vs. `PopulationNeeds`.
- **The Calculation:** $Price = BaseValue \times (1 + (Need / Supply))$.
- **Visual Scripting Implementation:** The `MarketSimulationGraph` recalculates this value every time a player completes a transaction or a "Colony Cycle" ticks.

### B. Arbitrage & Friction
- **Trade Route Efficiency:** A variable (0.0 to 1.0) that acts as a tax on transactions. 
- **The "Action Tax":** Low efficiency increases the spread between Buy and Sell prices, forcing the player to optimize logistics before scaling trades.

## 2. Narrative & Systemic Benchmarks
- **Disco Elysium (Systemic Dialogue):** Narrative is not a "reward" for gameplay; it is the gameplay. PVS aims to replicate the "Thought Cabinet" feel by using the `ColonyStressLevel` to filter which dialogue nodes are accessible.
- **Citizen Sleeper (Resource Survival):** The "Clock" and "Cycle" mechanics inform the `Stipend` delivery system.
- **Sovereign Systems:** The goal is to build a "Black Box" of logic that can be dropped into any visual medium (Unity, Godot, or even a Web-App) while maintaining the same economic integrity.

## 3. The "Five Archetype" Translation
Every raw data point in the WST must be translatable into a "Human State" before reaching Yarn Spinner:
1. **Prosperity:** (High Stability / Low Scarcity)
2. **Desperation:** (Low Stability / High Scarcity)
3. **Conflict:** (High Stress / Low Reputation)
4. **Discovery:** (High Focus / New Data Points)
5. **Stagnation:** (Low Focus / High Efficiency)

## 4. Technical Reference Documentation
- **Unity Visual Scripting API:** Documentation for `Custom Nodes` and `State Graph` transitions.
- **Yarn Spinner Documentation:** Standards for `Variable Injections` and `Command Callbacks`.
- **C-Core Documentation:** High-performance math libraries for floating-point market stability.