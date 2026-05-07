# Logic Blueprint: MarketSimulationGraph

## 1. Functional Role
This graph is the **Price-Setter**. It observes trade activity and environmental modifiers to calculate real-time values for Ore, Energy, and Pharmaceuticals. It ensures the economy is a "Fair Market"—transparent, predictable, but reactive.

## 2. Logic Flow & Node Architecture

### A. The Calculation Cycle (On Update/Tick)
1.  **Poll Scarcity:** Pull `Inventory_Indices` (Supply/Demand) from the **World State Table (WST)**.
2.  **Apply Modifiers:** - Pull `TradeRouteEfficiency`.
    - Pull `MarketInflationRate`.
3.  **Execute C-Core Math:** Call the `MarketClearing.c` library via a Custom Node to run the Supply-Demand curve algorithm.
4.  **Write Result:** Update `item_prices` in the WST.

### B. The Transaction Logic (On Purchase/Sale)
When the player interacts with a terminal or vendor, this graph executes the **Exchange Protocol**:
- **Inventory Check:** Does the player have the credits (for Buying) or the units (for Selling)?
- **Atomic Swap:** 1. Subtract/Add Credits.
    2. Add/Subtract Inventory units.
    3. **The Ripple:** Increment the `Demand` or `Supply` value in the WST immediately.
- **Price Shift:** Trigger an immediate recalculation of that specific item’s price to simulate market reaction.

### C. Arbitrage & Friction Logic
- **The Spread:** Calculates a Buy/Sell spread based on `TradeRouteEfficiency`. High efficiency = narrow spread; Low efficiency (Lockdown) = massive spread.
- **Bulk Penalty:** Implements a logic gate where selling massive quantities of a single resource exponentially crashes the price for that specific "Colony Cycle."

## 3. Visual Layout Standards
- **Green Groups:** Credit/Currency calculations.
- **Blue Groups:** Inventory & Resource management.
- **Purple Groups:** The Math Engine (C-Core Interop).
- **Orange Groups:** Feedback loops (Updating UI text and Merchant reactions).

## 4. GTM Methodology Alignment
This graph emulates a **Dynamic Pricing Engine**. It demonstrates how to build a system that responds to market signals (player actions) and internal health metrics (scarcity) to maintain an automated, balanced ecosystem. It is the ultimate expression of **Systemic Cause-and-Effect**.