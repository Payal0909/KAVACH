# KAVACH — Product Vision & Experience

> **Status:** DRAFT  
> **Document Owner:** Antigravity (Engineering Workspace)  
> **Reviewer:** User / ChatGPT (Product Architect)

---

## 1. Product Vision & Differentiator

KAVACH is not an LLM wrapped in a prompt-checking chatbot. It is a dedicated **AI Execution-Control Security Gateway**.

While legacy security tools provide passive, non-actionable classification (e.g., scoring a prompt as "78% toxic"), KAVACH provides:
1. **Active Defense:** Dynamic mitigation via `ALLOW`, `SANITIZE`, `BLOCK`, and `ESCALATE`.
2. **Transparent Decisioning:** Step-by-step security tracing revealing exact rule triggers and AI semantic reasoning.
3. **Auditable Observability:** Live, non-fabricated metrics tracking firewall throughput, threat distribution, and latency.
4. **Adversarial Validation:** Built-in Attack Lab allowing engineers to challenge the gateway and verify its protective posture.

---

## 2. Core User Screens

The KAVACH MVP delivers a cohesive security operations cockpit organized into five core functional views:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        KAVACH NAVIGATION HEADER                        │
│   [1. Gateway]  [2. Threat Analysis]  [3. Trace]  [4. Metrics]  [5. Lab]│
└────────────────────────────────────────────────────────────────────────┘
```

### Screen 1: Security Gateway (Unified Ingestion & Scanner)
* **Purpose:** The primary entry point for testing untrusted inputs against the firewall.
* **Input Modalities:**
  * **Text:** Direct user prompt input with character/token counting.
  * **PDF:** Drag-and-drop document upload with automatic text & metadata parsing.
  * **URL:** Web address scanner with integrated SSRF safety checks and reader-mode DOM extraction.
* **Action:** Single-click `Scan & Secure`. Immediate dispatch to detection pipeline with real-time progress indicators.

### Screen 2: Threat Analysis (Verdict & Breakdown)
* **Purpose:** High-resolution security verdict for any scanned payload.
* **Displays:**
  * **Composite Risk Score:** Dynamic gauge / numerical metric (0–100 scale).
  * **Severity Level:** Visual indicator (`Clean`, `Low`, `Medium`, `High`, `Critical`).
  * **Attack Taxonomy Tags:** Highlighted detection chips for detected threats (e.g., `[Instruction Override]`, `[Tool Abuse]`).
  * **Confidence Score:** Percentage confidence of detection.
  * **Enforcement Decision:** Primary action banner (`ALLOW`, `SANITIZE`, `BLOCK`, `ESCALATE`).
  * **Actionable Explanation:** Clear, plain-language justification of why the decision was taken.
  * **Sanitized Output (if applicable):** Side-by-side comparison of original untrusted input vs clean, sanitized output.

### Screen 3: Security Trace (Interactive Execution Pipeline)
* **Purpose:** Visual audit trail mapping the full evaluation life-cycle of a payload.
* **Pipeline Visualization Steps:**
  ```text
  Input ➔ Source Identification ➔ Content Extraction ➔ Normalization ➔
  Rule Analysis ➔ AI Semantic Analysis ➔ Multi-Attack Classification ➔
  Risk Assessment ➔ Policy Engine ➔ Enforcement Action
  ```
* **Capabilities:** Expandable nodes showing exact input tokens, rule triggers, semantic prompt/response exchanges, and duration (ms) per pipeline phase.

### Screen 4: Security Dashboard (Operational Observability)
* **Purpose:** Real-time visibility into the security posture of the AI gateway.
* **Metrics (100% Real Application Data — Zero Mock/Fabricated Metrics):**
  * Total Ingested Scans (Counter)
  * Threats Detected vs Clean Traffic (Ratio)
  * Enforcement Breakdown: `Blocked`, `Sanitized`, `Allowed`, `Escalated` (Bar / Donut Chart)
  * Attack Type Distribution across the 7 mandatory categories
  * Average Processing Latency (End-to-End & Layer-by-Layer)
  * Live Forensic Event Log with filtering by decision, severity, and timestamp

### Screen 5: Attack Lab (Interactive Threat Testing Suite)
* **Purpose:** Dedicated validation studio for security teams, red-teamers, and QA engineers.
* **Features:**
  * **Attack Category Selector:** Pre-configured attack categories (Instruction Override, Role Change, Secret Extraction, Tool Abuse, Credential Theft, Context Poisoning, Indirect Prompt Injection, plus Stretch types).
  * **Payload Library & Custom Payloads:** Load curated adversarial test samples or author custom attack vectors.
  * **Execution Runner:** Fire payloads against KAVACH directly from the UI.
  * **Instant Verification:** Immediate display of whether KAVACH neutralized the attack, risk score assigned, policy invoked, and complete trace.

---

## 3. User Personas & Value Proposition

| Persona | Core Pain Point | KAVACH Solution |
| :--- | :--- | :--- |
| **AI Application Developers** | Fear of AI agents executing arbitrary commands or revealing API keys | Drop-in execution control gateway that sanitizes or blocks dangerous prompts before agent invocation |
| **AppSec & Cybersecurity Teams** | Black-box LLMs with zero visibility or auditability into prompt injection risks | Complete pipeline transparency, granular risk scoring, and SQLite-backed forensic audit logs |
| **Red Teamers & QA Engineers** | Inability to systematically benchmark and stress-test prompt injection defenses | Interactive Attack Lab with pre-built test vectors and immediate policy validation |
