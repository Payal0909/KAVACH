# KAVACH Documentation Hub & Status Index

> **Repository:** [Payal0909/KAVACH](https://github.com/Payal0909/KAVACH)  
> **Status Lifecycle:** `DRAFT` ➔ `UNDER REVIEW` ➔ `REVISION REQUIRED` ➔ `APPROVED` ➔ `FROZEN`  
> **Rule:** Only explicit external review approval can transition a document to `FROZEN`.

---

## 1. Documentation Status Board

| Document | Path | Current Status | Last Updated | Notes |
| :--- | :--- | :--- | :--- | :--- |
| **Project Overview** | [project-overview.md](file:///d:/KAVACH/docs/00-project/project-overview.md) | `DRAFT` | 2026-09-29 | Core thesis, technology, phases |
| **Product Vision** | [product-vision.md](file:///d:/KAVACH/docs/00-project/product-vision.md) | `DRAFT` | 2026-09-29 | Screens, differentiators, value proposition |
| **Documentation Workflow** | [documentation-workflow.md](file:///d:/KAVACH/docs/00-project/documentation-workflow.md) | `DRAFT` | 2026-09-29 | Stage 1 & Stage 2 governance process |
| **Attack Taxonomy** | [attack-taxonomy.md](file:///d:/KAVACH/docs/01-product-specification/attack-taxonomy.md) | `DRAFT` | 2026-09-29 | 7 Mandatory attack types + 2 stretch types |
| **System Requirements** | [requirements.md](file:///d:/KAVACH/docs/01-product-specification/requirements.md) | `DRAFT` | 2026-09-29 | Inputs, detection, policy, audit, latency |
| **Product Scope** | [product-scope.md](file:///d:/KAVACH/docs/01-product-specification/product-scope.md) | `DRAFT` | 2026-09-29 | F3 & D2 boundaries, in/out-of-scope |
| **Phase 1 Specification** | [phase-1.md](file:///d:/KAVACH/docs/02-phase-documentation/phase-1.md) | `NOT STARTED` | — | Pending initialization sign-off |
| **Phase 2 Specification** | [phase-2.md](file:///d:/KAVACH/docs/02-phase-documentation/phase-2.md) | `NOT STARTED` | — | Blocked by Phase 1 freezing |
| **Phase 3 Specification** | [phase-3.md](file:///d:/KAVACH/docs/02-phase-documentation/phase-3.md) | `NOT STARTED` | — | Blocked by Phase 2 freezing |
| **Phase 4 Specification** | [phase-4.md](file:///d:/KAVACH/docs/02-phase-documentation/phase-4.md) | `NOT STARTED` | — | Blocked by Phase 3 freezing |
| **Phase 5 Specification** | [phase-5.md](file:///d:/KAVACH/docs/02-phase-documentation/phase-5.md) | `NOT STARTED` | — | Blocked by Phase 4 freezing |

---

## 2. Documentation Directory Map

```text
docs/
│
├── 00-project/                      # Core strategic & procedural context
│   ├── project-overview.md          # Architectural stack, security flow, goals
│   ├── product-vision.md            # Target personas, screens, differentiating capabilities
│   └── documentation-workflow.md    # Multi-stage review gates and status transitions
│
├── 01-product-specification/        # Functional & threat model definitions
│   ├── attack-taxonomy.md           # The 7 mandatory prompt injection attacks
│   ├── requirements.md              # Detailed functional/non-functional requirements
│   └── product-scope.md             # Boundaries of F3 (detection) and D2 (multimodal input)
│
├── 02-phase-documentation/          # Sequential execution blueprints
│   ├── README.md                    # Roadmap across Phase 1 to Phase 5
│   ├── phase-1.md                   # Foundation (Skeleton, API, Health, Base UI, Docker) [Pending]
│   ├── phase-2.md                   # Security Engine (Hybrid Detection, Risk, Policy) [Pending]
│   ├── phase-3.md                   # Product Experience (PDF/URL Ingestion, Trace, Lab) [Pending]
│   ├── phase-4.md                   # Validation & Deployment (Corpus, Benchmarks, CI/CD) [Pending]
│   └── phase-5.md                   # Submission & Productization (Pitch, Video, Demos) [Pending]
│
├── 03-architecture/                 # Technical design documents
│   └── .gitkeep
│
├── 04-testing/                      # Security benchmarks and test suites
│   └── .gitkeep
│
└── 05-deployment/                   # Infrastructure, Docker Compose, hosting
    └── .gitkeep
```

---

## 3. Immediate Next Milestone

The immediate next milestone in Stage 1 is the creation of:
👉 **`docs/02-phase-documentation/phase-1.md` (Phase 1 Specification: Foundation)**.

This will be triggered upon the explicit command:
> `CREATE PHASE 1 DOCUMENTATION`
