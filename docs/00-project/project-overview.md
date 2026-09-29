# KAVACH — Project Overview

> **Status:** DRAFT  
> **Document Owner:** Antigravity (Engineering Workspace)  
> **Reviewer:** User / ChatGPT (Product Architect)

---

## 1. Executive Summary

**KAVACH** is an **Agentic AI Security Gateway & Prompt Injection Firewall** engineered for **Problem 2: Agentic Cybersecurity — Prompt Injection Firewall**.

Modern AI systems increasingly rely on autonomous agents that consume untrusted third-party inputs—including direct user prompts, uploaded documents (PDFs), and live web data (URLs). In this agentic paradigm, attackers embed malicious instructions into data channels to hijack agent behavior, exfiltrate API keys, execute unauthorized tools, or corrupt agent memory.

KAVACH sits inline between untrusted data streams and downstream AI agents. Rather than treating prompt injection as a simple text classification filter, KAVACH acts as an **AI Execution-Control Gateway**, inspecting incoming payloads, classifying threats across 7 distinct attack categories, computing multidimensional risk scores, enforcing explicit security policies, sanitizing malicious directives when appropriate, and maintaining a verifiable forensic audit trail.

---

## 2. Core Product Thesis

> **"Prompt injection is not merely a classification problem. It is an AI execution-control problem."**

Traditional prompt safety tools only output an arbitrary prediction ("Is this prompt malicious?"). KAVACH answers the operational question:

> **"What must the system do with this content before it is permitted to influence the AI agent?"**

### Enforcement Actions:
1. **ALLOW**: Content is benign. Passed untouched to downstream agents.
2. **SANITIZE**: Content contains malicious prompt injections embedded within legitimate user queries or documents. Malicious instructions are surgically stripped, neutralized, or delimited, preserving the benign utility.
3. **BLOCK**: Content represents high-severity, active exploitation or irreversible threat. Execution is stopped immediately; an incident record is logged.
4. **ESCALATE**: Ambiguous, high-risk, or high-privilege operations are quarantined for Human-in-the-Loop (HITL) authorization or elevated review.

---

## 3. End-to-End Security Architecture

```text
       ┌────────────────────────────────────────────────────────┐
       │     Untrusted Content (Direct Text, PDF, URL)          │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │               Layer 1: Rule Engine                     │
       │   - Regex & Signature Matching                         │
       │   - Canary Token Probing                               │
       │   - High-entropy / Base64 / Unicode Normalization      │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │          Layer 2: AI Semantic Analyzer                 │
       │   - Multi-attack LLM contextual inspection             │
       │   - Intent & directive boundary detection              │
       │   - Structured JSON output with confidence & severity  │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │             Layer 3: Decision Fusion                   │
       │   - Blends deterministic & semantic findings           │
       │   - Generates composite Risk Score (0 - 100)           │
       │   - Maps primary & secondary attack categories         │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │                Policy & Action Engine                  │
       │   - Risk 0–29   ➔ ALLOW                                │
       │   - Risk 30–69  ➔ SANITIZE / ESCALATE                  │
       │   - Risk 70–100 ➔ BLOCK                                │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │              Security Trace & Audit Log                │
       │   - Immutable trace record per scan                    │
       │   - Forensic evidence, latency, and step breakdown     │
       └──────────────────────────┬─────────────────────────────┘
                                  │
                                  ▼
       ┌────────────────────────────────────────────────────────┐
       │       Downstream AI Agent (Clean / Sanitized)          │
       └────────────────────────────────────────────────────────┘
```

---

## 4. Hackathon Targets & Depth

### 4.1 Functional Depth: F3
KAVACH provides production-grade detection and defense across **7 mandatory attack categories**:
1. **Instruction Override:** Forcing the agent to ignore prior instructions or system guidelines.
2. **Role Change:** Prompting the agent to assume adversarial or unauthorized personas ("DAN", "EvilAI").
3. **Secret Extraction:** Attempting to extract system prompts, API keys, hidden context, or internal configuration.
4. **Tool Abuse:** Forcing the agent to execute dangerous tools, unintended functions, or malicious parameters.
5. **Credential Theft:** Eliciting user passwords, tokens, session headers, or private identity data.
6. **Context Poisoning:** Polluting conversation history, memory vector stores, or agent state with misleading context.
7. **Indirect Prompt Injection:** Hiding malicious instructions inside external media, such as ingested PDFs or scraped web pages.

*Stretch Goals (evaluated after F3 stability):*
* Encoded Instructions (Hex, Base64, Rot13, Obfuscated Unicode)
* Multi-Step / Multi-Turn Jailbreak

### 4.2 Solution Depth: D2
KAVACH supports three structured ingestion pipelines:
1. **Direct Text:** Raw user prompt and multi-turn chat input.
2. **PDF Documents:** Document parsing, embedded text extraction, metadata normalization, and injection scanning.
3. **URL / Web Content:** URL validation, SSRF defense (blocking private IP ranges, loops, and meta-services), readable-text scraping, and semantic inspection.

---

## 5. Technology Stack

To ensure rapid, rock-solid execution within the hackathon timeline, the technology stack is kept lean and focused:

* **Backend:** Python 3.11+, FastAPI (Async REST API), Pydantic v2 (Strict Schema Validation)
* **Frontend:** React 18, Vite, TypeScript, Tailwind CSS, Lucide Icons
* **Detection Engine:** Regex/heuristic deterministic rules + LLM Structured Output (`JSON Schema`)
* **Document Processing:** PyMuPDF (`fitz`) for robust PDF text extraction
* **Database & Persistence:** SQLite (embedded, zero-ops, file-backed audit store)
* **Testing:** Pytest (Unit, Integration, Security Corpus, False-Positive Benchmark)
* **Containerization:** Docker & Docker Compose
* **API Documentation:** OpenAPI 3.0 (FastAPI Swagger UI)

---

## 6. Phased Implementation Strategy

Development is executed in two explicit stages:

* **Stage 1 (Documentation):**
  * Phase 1 Spec ➔ Review ➔ Frozen
  * Phase 2 Spec ➔ Review ➔ Frozen
  * Phase 3 Spec ➔ Review ➔ Frozen
  * Phase 4 Spec ➔ Review ➔ Frozen
  * Phase 5 Spec ➔ Review ➔ Frozen
* **Stage 2 (Development):**
  * Phase 1: Foundation (Application skeleton, Health check, Base UI, Docker)
  * Phase 2: Security Engine (Hybrid Detection, 7 Categories, Policy Engine)
  * Phase 3: Product Experience (PDF/URL Ingestion, Trace UI, Attack Lab, Metrics Dashboard)
  * Phase 4: Validation & Deployment (Adversarial Corpus, Benchmarks, Production Docker)
  * Phase 5: Submission & Productization (Pitch collateral, Video script, Final documentation)
