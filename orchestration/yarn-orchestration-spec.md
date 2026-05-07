# Technical Specification: Yarn Spinner as a Narrative API

## 1. The "Why": Orchestration vs. Scripting
In **PROXIMITY-Visual-Scripting**, we do not "write stories"; we "architect outcomes." Standard dialogue tools are too rigid for a high-performance mercantile simulation. We use Yarn Spinner because it functions as a **Narrative API**—a bridge between raw data and human-readable output.

### Key Advantages:
- **Statelessness:** Yarn Spinner doesn't need to track player history; it simply queries the current **World State Table (WST)** and responds to the "Now."
- **Logic-Inside-Text:** It allows us to embed conditional logic (`<<if>>` statements) directly into the dialogue files, reducing the need for massive, messy node graphs in Unity for every minor conversation.
- **Action Tax Reduction:** By separating the "writing" (Yarn) from the "math" (C-Core/UVS), we allow for rapid iteration on the game's tone without touching the core simulation code.

## 2. The "How": The Pull-Protocol
The integration follows a strict data-flow pipeline:

1.  **The Trigger:** The player enters an NPC's proximity.
2.  **The Query:** The Unity Visual Scripting (UVS) layer calls the Yarn script.
3.  **The Pull:** Before the first line of text appears, Yarn executes "Command Callbacks" to the WST (e.g., `get_wst_value`).
4.  **The Injection:** The variables are injected into the text (e.g., `"The price of Ore is {$ore_price}"`).
5.  **The Presentation:** The final, context-aware string is served to the UI.

## 3. Systemic Dialogue Archetypes
To maintain consistency, all Yarn scripts must utilize the **Five Archetype Translation** logic defined in `references.md`. 
- **Prosperity Scripts:** Focus on greed and expansion.
- **Desperation Scripts:** Focus on survival and high-cost trades.
- **Conflict Scripts:** Focus on tension and reputation gates.

## 4. GTM Alignment: The "Sales Enablement" Analogy
In a GTM environment, you don't give a salesperson a static script; you give them a **Dynamic Playbook** that changes based on the lead's industry, budget, and pain points. Yarn Spinner is the "Playbook" of the PVS framework—ensuring the "Customer" (the Player) receives the most relevant information based on the "Account Data" (the World State).