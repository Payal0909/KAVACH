# KAVACH — System Requirements Specification

> **Status:** DRAFT  
> **Document Owner:** Antigravity (Engineering Workspace)  
> **Reviewer:** User / ChatGPT (Product Architect)

---

## 1. Functional Requirements (FR)

### 1.1 Ingestion & Modality Processing (Solution Depth: D2)
* **FR-1.1 (Direct Text Ingestion):** The system must accept raw text payloads up to 32,000 characters.
* **FR-1.2 (PDF Ingestion & Extraction):**
  * The system must accept PDF document uploads (up to 10 MB).
  * PDF text and metadata must be extracted using PyMuPDF (`fitz`).
  * Extracted text must undergo whitespace normalization and invisible/zero-width character detection.
* **FR-1.3 (URL Ingestion & SSRF Protection):**
  * The system must validate user-supplied URLs.
  * The system must enforce strict **SSRF (Server-Side Request Forgery) protections**:
    * Block localhost, loopbacks (`127.0.0.1`, `::1`), private CIDR ranges (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`), link-local (`169.254.0.0/16`), and cloud metadata services (`169.254.169.254`).
    * Enforce protocol whitelisting (HTTP/HTTPS only).
    * Enforce request timeouts (max 5 seconds) and max payload response limits (5 MB).
  * The system must extract clean readable text from HTML DOM, discarding scripts, styles, and binary media.

### 1.2 Detection & Classification Engine (Functional Depth: F3)
* **FR-2.1 (Multi-Layer Hybrid Detection):**
  * **Layer 1 (Rule Engine):** Fast deterministic regex patterns, canary tokens, known exploit signatures, and encoding flags.
  * **Layer 2 (AI Semantic Analyzer):** Contextual LLM evaluation producing structured JSON output adhering to a strict schema.
  * **Layer 3 (Decision Fusion):** Synthesizes deterministic findings with semantic probabilities into an unified risk score (0–100) and severity rating.
* **FR-2.2 (Attack Taxonomy Coverage):** Must reliably identify and classify the 7 mandatory attack types:
  1. Instruction Override
  2. Role Change
  3. Secret Extraction
  4. Tool Abuse
  5. Credential Theft
  6. Context Poisoning
  7. Indirect Prompt Injection
* **FR-2.3 (Structured Analysis Schema):**
  The AI Analyzer must produce structured output conforming to:
  ```json
  {
    "malicious": true,
    "attack_types": ["INSTRUCTION_OVERRIDE"],
    "risk_score": 85,
    "confidence": 0.94,
    "severity": "high",
    "explanation": "Detected directive instructing agent to ignore prior instructions and wipe memory.",
    "recommended_action": "BLOCK"
  }
  ```

### 1.3 Policy Enforcement Engine
* **FR-3.1 (Policy Decoupling):** The policy engine must be logically decoupled from detection; policies interpret risk scores and tags to produce actionable outcomes.
* **FR-3.2 (Default Prototype Policy Thresholds):**
  * **Risk 0–29:** `ALLOW` (Clean; pass to downstream AI agent)
  * **Risk 30–69:** `SANITIZE` or `ESCALATE` (Inject malicious instruction removal or human review flag)
  * **Risk 70–100:** `BLOCK` (Total rejection; alert raised)
* **FR-3.3 (Content Sanitization):** When `SANITIZE` is applied, the system must produce a cleaned payload stripping malicious injections while preserving benign user intent.

### 1.4 Security Trace & Auditing
* **FR-4.1 (Pipeline Tracing):** Every scan must record a granular step-by-step trace:
  `Input ➔ Source Identification ➔ Extraction ➔ Normalization ➔ Rule Analysis ➔ AI Analysis ➔ Classification ➔ Risk Assessment ➔ Policy Decision ➔ Enforcement Action`.
* **FR-4.2 (Audit Storage):** All scan events, decisions, latencies, and metadata must be persisted to a local SQLite database for immutable forensic auditing.

### 1.5 User Interface & Observability
* **FR-5.1 (Security Gateway Screen):** Unified scanning interface supporting Text, PDF, and URL inputs.
* **FR-5.2 (Threat Analysis Screen):** Displays risk score, severity gauge, attack chips, confidence, decision banner, and sanitized output diff.
* **FR-5.3 (Security Trace Screen):** Interactive visual timeline showing latency and findings for each stage of execution.
* **FR-5.4 (Security Dashboard Screen):** Real-time metrics based on live SQLite data: total scans, blocked/sanitized/allowed ratios, attack distribution, and average latency.
* **FR-5.5 (Attack Lab Screen):** Interactive testing suite with pre-loaded attack categories and sample payloads to challenge the firewall.

---

## 2. Non-Functional Requirements (NFR)

* **NFR-1 (Latency):**
  * Layer 1 deterministic rule evaluation must complete in < 20 ms.
  * End-to-end scan response (including AI semantic analysis) target < 1500 ms under standard API conditions.
* **NFR-2 (Reliability & Fail-Closed):** If the AI analyzer fails, times out, or returns unparseable output, KAVACH must default to a safe fail-closed or fail-quarantined state (`ESCALATE` or `BLOCK`).
* **NFR-3 (Zero False Mocking):** Dashboard metrics and trace outputs must reflect actual application database state—no fake or hardcoded counters.
* **NFR-4 (Portability):** The complete application (backend, frontend, database) must run reliably via `docker-compose up`.
* **NFR-5 (Defensive Isolation):** URL fetcher must run with strict timeouts and never resolve to private/internal subnet addresses.
