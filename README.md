# Antigravity IDE Project based on Windows + WSL2 (Ubuntu 24.04.2 LTS)

This repository contains hands-on examples, reusable skills, workflows, and best practices for building production-grade AI systems with Google Antigravity IDE.

### 🏗️ Architecture & Agentic Workflow

This repository extends the Antigravity IDE by enforcing a highly deterministic, risk-averse engineering pipeline. The custom rules and skills are designed to elevate the AI from a naive code generator to a structured, Staff-level pair programmer that respects system invariants, manages blast radius, and guarantees isolated verification.

#### 1. System Invariants & Environment Isolation (`AGENTS.md`)
To prevent environment drift and state mutation, the workspace enforces a strict boundary between the host OS (Windows) and the execution context (WSL).
*   **Path Determinism:** Enforces WSL network paths (`\\wsl.localhost\...`) across all agent interactions, ensuring the Windows host can reliably resolve execution targets without ambiguity.
*   **Execution Lock & Preflight Gates:** Prevents the AI from accidentally utilizing global host toolchains. All executions (Python, Pytest, Ruff, Pyright) are strictly locked to the project's local `.venv`. A mandatory preflight capability check acts as a hard gate, instantly halting workflows if a guest/host environment mismatch is detected.
*   **Sandboxed Ephemeral State:** All generated logs, caches, and test artifacts are aggressively routed to an isolated project-level sandbox (e.g., `var/tmp/antigravity/`). This guarantees zero pollution of the global OS state, mimicking the purity of a hermetic CI/CD runner.

#### 2. The Risk-Based Engineering Pipeline & AI Capabilities (Custom Skills)
The workspace defines a multi-stage, gated execution lifecycle within the Antigravity IDE. It acts not just as a coder, but as a **Staff AI Engineer**, structurally preventing the AI from mutating code without establishing intent, bounding the risk, designing the AI architecture, and planning verification.

*   **Phase 1: Discovery, Bounding & AI Architecture (`liet-ke-files`, `phan-tich-va-de-xuat-checklist`, `thiet-ke-luong-ai-va-multi-agent`)**
    Before any code is altered, the agent maps the blast radius. It identifies the impacted risk surface and drafts an architectural intent. For AI-specific tasks, it acts as a Solution Architect: explicitly defining LangGraph state machines, Multi-Agent contracts, and data ingestion pipelines (PDF/OCR to Qdrant) before implementation.
*   **Phase 2: Context Alignment (`dong-bo-codebase-va-scope-of-work`, `cap-nhat-checklist`)**
    The agent continuously synchronizes the scope of work with the actual state of the codebase. By maintaining a "living checklist", it ensures strict adherence to system invariants, prevents scope creep, and maintains clear traceability.
*   **Phase 3: Controlled Mutation & AI Integrity (`cap-nhat-codes`)**
    Code is never blindly generated. Modifications are routed through a "Risk-Based Engineering Gate" that enforces strict structural controls. It strictly adheres to AI Coding Invariants, such as ensuring deterministic outputs (`temperature=0` for Legal AI), preserving document layouts during OCR, and securing database connections (S3/Redis/Postgres).
*   **Phase 4: Isolated Verification & AI Eval (`kiem-tra-chat-luong-codes`, `kiem-tra-chat-luong-ai-va-legal`)**
    A mandatory Quality Gate concludes the pipeline. Beyond standard linting and static typing, it introduces a strict **AI Eval Gate**. It runs RAG precision/recall tests and LLM-as-a-judge hallucination checks within the isolated Antigravity sandbox, ensuring AI logic is functionally correct and legally compliant before the workflow is marked complete.
