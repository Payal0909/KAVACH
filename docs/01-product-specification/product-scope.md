# KAVACH — Product Scope & Boundaries (F3 / D2)

> **Status:** DRAFT  
> **Document Owner:** Antigravity (Engineering Workspace)  
> **Reviewer:** User / ChatGPT (Product Architect)

---

## 1. Hackathon Scope Targets

KAVACH is calibrated specifically for hackathon evaluation:
* **Functional Depth: F3** — Multi-category prompt injection detection across **seven mandatory attack types**.
* **Solution Depth: D2** — Structured multimodal input ingestion covering **Direct Text, PDF Documents, and Web URLs**.

We do **not** claim Solution Depth D3 (audio, video, real-time binary streaming) or custom-trained foundation models unless explicitly implemented and verified.

---

## 2. In-Scope Deliverables (MVP Baseline)

### 2.1 Ingestion Modalities (D2)
* **Direct Text:** Raw textual prompts, system instructions, and multi-turn chat dialogues.
* **PDF Documents:** Parsing text, extracting metadata, stripping whitespace anomalies via PyMuPDF.
* **URL Content:** Validated web address retrieval, SSRF prevention, HTML stripping, and DOM text normalization.

### 2.2 Attack Coverage (F3)
* **Instruction Override**
* **Role Change**
* **Secret Extraction**
* **Tool Abuse**
* **Credential Theft**
* **Context Poisoning**
* **Indirect Prompt Injection**
* *(Stretch: Encoded Instructions, Multi-Step Jailbreak)*

### 2.3 Core System Capabilities
* **Hybrid Security Engine:** Deterministic rule engine (Layer 1) + AI semantic analyzer (Layer 2) + Decision Fusion (Layer 3).
* **Policy Engine:** Configurable mapping from risk scores to actionable decisions (`ALLOW`, `SANITIZE`, `BLOCK`, `ESCALATE`).
* **Content Sanitization:** Surgical neutralization of malicious prompt injection directives while preserving clean context.
* **Security Tracing:** End-to-end audit trail exposing each transformation and decision point.
* **Observability Dashboard:** Live application metrics backed by local SQLite storage (no mocked numbers).
* **Attack Lab:** Interactive playground for testing custom or pre-packaged attack payloads.
* **Docker Packaging:** Fully functional multi-container Docker Compose setup for backend and frontend.

---

## 3. Explicitly Out-of-Scope (Non-Scope)

To maintain rapid velocity, reliability, and code quality, the following are strictly **NON-SCOPE** for this MVP:

* **No D3 Modalities:** Audio streaming, video frame inspection, image OCR steganography, or binary executable disassembly.
* **No Custom Model Training:** We will not fine-tune or train custom neural networks; we leverage deterministic heuristics combined with state-of-the-art LLM APIs using strict structured JSON schemas.
* **No Heavy Distributed Middleware:** No Apache Kafka, RabbitMQ, Celery, Redis cluster, or external message brokers.
* **No Vector Databases:** No Pinecone, Milvus, Qdrant, or Weaviate infrastructure.
* **No Microservices Orchestration:** No Kubernetes, Helm charts, service meshes (Istio/Linkerd), or multi-cloud topologies.
* **No Complex Enterprise Identity:** No OAuth2/SAML SSO, multi-tenant organization billing, or fine-grained RBAC hierarchies beyond standard local API keys or session tokens.

---

## 4. Scope Discipline & Boundary Enforcement

1. **Avoid Over-Engineering:** Every component must directly support the F3 / D2 targets or the 5 user screens.
2. **Defensive Simplicity:** A reliable, tested, and explainable prototype in SQLite and FastAPI is vastly superior to a buggy, half-finished distributed system.
3. **Traceability:** Any feature introduced during implementation must trace directly back to an approved and frozen phase specification.
