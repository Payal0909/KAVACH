# KAVACH — Agentic AI Security Gateway & Prompt Injection Firewall

> **Status:** DRAFT | **Hackathon Target:** Problem 2 (Agentic Cybersecurity — Prompt Injection Firewall) | **Functional Target:** F3 | **Solution Depth:** D2

---

## 1. Product Thesis

> **"Prompt injection is not merely a classification problem. It is an AI execution-control problem."**

Traditional security approaches treat prompt injection as a binary text classification task ("Is this prompt malicious?"). In real-world agentic environments, binary classification is insufficient.

**KAVACH** operates as an inline execution-control security gateway situated between untrusted external content and downstream AI agents. Instead of simply predicting maliciousness, KAVACH determines:

> **"What must the system do with this content before it is permitted to influence the AI agent?"**

### Core Enforcement Actions:
* **`ALLOW`**: Content is clean; pass through directly to downstream AI agents.
* **`SANITIZE`**: Content contains instructions or untrusted directives alongside legitimate payload; neutralize malicious instructions while preserving clean content.
* **`BLOCK`**: Content is hostile, irrecoverable, or high-risk; reject entirely and alert.
* **`ESCALATE`**: Ambiguous, high-impact, or anomalous payload; hold for human-in-the-loop (HITL) approval or stepped-up authentication.

---

## 2. Fundamental Security Flow

```text
UNTRUSTED CONTENT (Direct Text, PDF, URL)
   │
   ▼
[ DETECT ]          Deterministic signatures, regex patterns, canary tokens
   │
   ▼
[ CLASSIFY ]        AI Semantic Analyzer for contextual intent across 7 attack types
   │
   ▼
[ ASSESS RISK ]     Multi-factor scoring (Severity, Confidence, Context impact)
   │
   ▼
[ APPLY POLICY ]    Configurable risk thresholds and rule-action mapping
   │
   ▼
[ ACT ]             ALLOW | SANITIZE | BLOCK | ESCALATE
   │
   ▼
[ AUDIT ]           Immutable security trace and forensic event logging
   │
   ▼
AI AGENT            Protected downstream agent execution environment
```

---

## 3. Scope & Hackathon Targets

* **Functional Depth (F3):** Reliable multi-class detection across **7 mandatory attack categories**:
  1. **Instruction Override**
  2. **Role Change**
  3. **Secret Extraction**
  4. **Tool Abuse**
  5. **Credential Theft**
  6. **Context Poisoning**
  7. **Indirect Prompt Injection**
  *(Optional stretch: Encoded Instructions, Multi-Step Jailbreak)*
* **Solution Depth (D2):** Structured multimodal ingestion:
  1. **Direct text** input
  2. **PDF documents** (Text extraction + layout normalization)
  3. **URL / Web content** (Validation + SSRF protection + readable-text extraction)

---

## 4. Documentation-First Methodology

This repository is governed by a strict **Documentation-First Workflow**:
1. **Stage 1 (Documentation):** All 5 phases are formally specified, peer-reviewed, and frozen before writing application code.
2. **Stage 2 (Development):** Phased implementation strictly adhering to frozen specifications.

See [Documentation Hub](file:///d:/KAVACH/docs/README.md) and [Documentation Workflow](file:///d:/KAVACH/docs/00-project/documentation-workflow.md) for full protocol details.

---

## 5. Documentation Directory Structure

```text
docs/
├── 00-project/
│   ├── project-overview.md       # High-level architecture, thesis, and stack
│   ├── product-vision.md         # Product differentiators, user screens, value prop
│   └── documentation-workflow.md # Phase documentation and review governance
├── 01-product-specification/
│   ├── requirements.md           # Functional & non-functional requirements
│   ├── attack-taxonomy.md        # Comprehensive 7-category threat model
│   └── product-scope.md          # MVP scope boundaries (F3 / D2)
├── 02-phase-documentation/       # Phase 1 through 5 formal engineering plans
├── 03-architecture/              # Architectural diagrams and decision records (ADRs)
├── 04-testing/                   # Security test corpus & adversarial benchmarks
└── 05-deployment/                # Docker & production readiness guides
```

For status on all specifications, refer to the [Documentation Index](file:///d:/KAVACH/docs/README.md).
