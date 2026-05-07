# Technical Specification: Unity Environment & Pipeline

## 1. The Environment Mandate
The Unity environment serves as the visual interface for the **World State Table (WST)**. Its primary role is to render the consequences of the mercantile simulation and provide the user with the necessary UI to interact with the C-Core logic.

## 2. Project Standards
- **Version:** Unity 2022.3 LTS (Long Term Support) to ensure API stability for the C-Core bridge.
- **Rendering Pipeline:** Universal Render Pipeline (URP). This provides high-performance visuals across a wide range of hardware without bloated "Action Tax" on the GPU.
- **Organization:** The project follows a "System-First" folder structure, mirroring the repository's logic rather than Unity's default assets-only approach.

## 3. Data Integration Pipeline
### A. The WST Observer
- Every interactive object (Terminal, NPC, Resource Node) must contain a **WST Observer Component**.
- This component is a Visual Scripting entry point that polls relevant variables from the WST at specific intervals (e.g., Every 1.0s or On-Enter-Radius).

### B. UI & Feedback Loop
- **Economic HUD:** Driven by a centralized `UIPresenterGraph`. It pulls `Credits`, `ItemPrices`, and `ColonyStressLevel` to update the player’s dashboard.
- **Visual Feedback:** We use **Material Property Blocks** driven by Visual Scripting to change environment colors (e.g., lighting shifts to an amber warning hue as `ColonyStability` drops).

## 4. Asset Guidelines
- **UI Aesthetic:** "Terminal-Industrial." High contrast, text-heavy, and data-centric.
- **NPC Archetypes:** NPCs are prefabs with a standardized `NPCDialogueGraph`. The specific character identity is "injected" via the WST at runtime.
- **Optimization:** All environmental data is baked where possible. Real-time compute cycles are strictly reserved for the **Mercantile Engine** and **Agent Orchestration**.

## 5. GTM Methodology Alignment
This pipeline demonstrates **Operational Efficiency**. By standardizing how data is surfaced from the WST to the UI, we eliminate manual, one-off scripting tasks. This mirrors a scalable GTM dashboard where any new metric can be added to the source data and automatically reflected in the visual output.