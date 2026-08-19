# Engineering & Design Decisions — Track 2: Premium Home Page

**Candidate:** Piyush Raj  
**Project:** AcdyOn AgentOS (`agentos.acdyon.tech`)  
**Deployment:** Vercel / GitHub Pages  

---

### 1. Why this UI/Ingestion Strategy over the Obvious Alternative?

Instead of building a conventional "marketing-brochure" landing page with static mockup graphics or placeholder screenshots, I built a **deterministic, interactive pipeline simulator** directly into the hero experience.

* **Instant Verification of Value:** In the first 3 seconds, a developer or engineering lead needs to see how the engine handles state transitions, data ingestion, and deterministic tool calls. The interactive simulator (`Execute Workflow`) visualizes the telemetry lifecycle from fingerprint rotation to semantic caching and authenticated tool execution in real time.
* **Zero Bloat & Performance-First Architecture:** Rather than introducing heavy external dependencies, I used semantic HTML5, utility-first Tailwind CSS, Lucide icons, and optimized vanilla JS execution loops. This ensures sub-millisecond initial page loads, crisp dark-mode contrast, and zero hydration layout shifts.

---

### 2. One Trade-off Made Under the Time Limit & 1-Week Roadmap

* **The Trade-off:** The real-time agent console uses client-side simulated state machine loops with deterministic timing delays rather than an active WebSocket pipe connected to a distributed backend execution cluster.
* **With a Full Week:**
  1. **Live WebSocket Stream:** Connect the execution console to a live sandboxed Python/FastAPI agent runtime that dispatches real API calls and displays live network latency.
  2. **Custom Agent DAG Builder:** Add a visual drag-and-drop node graph canvas where users can build multi-step agent topologies directly in the browser.
  3. **Automated Cross-Viewport Regression Suite:** Implement automated Playwright/Cypress end-to-end tests across 390px (mobile) through 1440px+ (desktop) viewports[cite: 1].

---

### 3. AI Tool Usage & Personal Engineering Verification

* **Where AI was Used:** AI was used to draft initial semantic components, generate realistic terminal event signatures, and verify CSS mathematical formulas for the dynamic slider calculator[cite: 1].
* **What I Personally Verified & Altered:**
  1. **Eliminated All Fabricated Proof:** Strictly enforced the brief's constraint by removing fake testimonial cards, fabricated partner logos, and generic rating stars, replacing them entirely with functional technical metrics[cite: 1].
  2. **Viewport Hardening:** Manually audited container bounds, flex layouts, and modal transforms to guarantee zero horizontal scroll on mobile (390px) and wide desktop (1440px) displays[cite: 1].
  3. **Interactive Logic & State Machine:** Personally debugged and bound the multi-stage asynchronous DOM update sequence (`triggerSimulatedRun`), the slider calculator logic, and the global keyboard shortcut (`Ctrl + K`) for the terminal Easter Egg[cite: 1].