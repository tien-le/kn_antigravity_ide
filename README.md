# Antigravity IDE: Staff-level AI Engineering Workspace

## 📌 TL;DR
This workspace upgrades the Antigravity IDE from a standard code generator into a **Staff-level AI Engineer**. It enforces a strict, deterministic, and risk-averse pipeline across a hybrid Windows-WSL environment by utilizing custom environment invariants (`AGENTS.md`), local agent skills, and global security plugins.

## 📦 What? (What is this repository?)
This repository defines the operational boundaries and execution lifecycles for AI-assisted development. It consists of three core pillars:
1. **Environment Invariants**: Hard rules (`AGENTS.md`) that dictate how paths, toolchains, and ephemeral states are handled to bridge Windows and WSL.
2. **Custom AI Skills**: Specialized local skills (e.g., `liet-ke-files`, `cap-nhat-codes`) that act as architectural, alignment, and quality gates.
3. **Advanced Security Integrations**: Deep hooks into the IDE's `securecoder` plugin ecosystem for threat modeling and dependency validation.

## 🎯 Why? (Why do we need this strict structure?)
*   **Prevent Environment Drift**: Windows and WSL (Ubuntu) file systems and binaries often clash. We enforce hard boundaries to prevent the AI from executing Windows `powershell` or polluting global host states.
*   **Prevent "Blind" AI Mutations**: Naive AI writes code first and asks questions later. A Staff-level AI must understand the architecture, define the blast radius, and sync context *before* modifying a single line of code.
*   **Zero-Trust Security & Quality**: AI-generated code introduces risks (hallucinations, logic flaws, vulnerable dependencies). We require isolated, deterministic quality gates (RAG accuracy, LLM-as-a-judge, CWE scanning) before accepting changes.

## ⏳ When? (When are these rules and skills applied?)
The invariants in `AGENTS.md` apply to **every single interaction**. The local skills are triggered systematically across four distinct lifecycle phases:
1.  **Before Coding (Discovery & Design):** When a task is assigned, the AI maps the risk surface, designs the multi-agent architecture, and synchronizes the scope of work.
2.  **During Coding (Controlled Mutation):** When writing code, the AI enforces structural invariants (e.g., preventing drift, managing dependencies).
3.  **Before Merging (Verification):** When the logic is complete, the AI runs isolated Pytest/Ruff checks and specialized AI evaluations.
4.  **When Adding Dependencies (Security):** The AI strictly scans packages and builds threat models before allowing new third-party libraries.

## 📍 Where? (Where does execution happen?)
Execution is heavily sandboxed to guarantee determinism and protect the host machine:
*   **Pathing**: Exclusively uses WSL network paths (`\\wsl.localhost\Ubuntu-2404\home\lavie\...`) or absolute Linux paths.
*   **Compute (Preflight Gate)**: Locked strictly to the local virtual environment. A Preflight Gate ensures the correct Python version (e.g., 3.12) is running via `.venv/bin/python`; otherwise, it throws a `python_preflight_error`.
*   **Storage (Sandbox Root)**: Ephemeral data (logs, pytest caches) is forcibly routed to `/home/lavie/dev/work/nhiem_vu/kn_antigravity_ide/var/tmp/codex/`. Global OS temp directories (`/tmp/` or Windows `Temp`) are strictly blocked.

## ⚙️ How? (How does the AI operate?)
The AI operates via a multi-stage **Risk-Based Engineering Pipeline**:
1.  **Phase 1 - Bounding & Architecture**: Uses `liet-ke-files`, `phan-tich-va-de-xuat-checklist`, and `thiet-ke-luong-ai-va-multi-agent` to establish intent and design LangGraph/Data pipelines.
2.  **Phase 2 - Context Alignment**: Uses `dong-bo-codebase-va-scope-of-work` and `cap-nhat-checklist` to sync the state without mutating code.
3.  **Phase 3 - Controlled Mutation**: Uses `cap-nhat-codes` to apply risk-mitigated code generation.
4.  **Phase 4 - Isolated Verification**: Uses `kiem-tra-chat-luong-codes` (lint/test) and `kiem-tra-chat-luong-ai-va-legal` (AI hallucination/legal checks).
5.  **Phase 5 - Security Lifecycle**: Uses `scan_dependencies` and `determine-threat-model` to validate external packages and secure the system architecture.

## 💡 Illustrated Example (Ví dụ minh họa)
**Scenario**: The user asks the agent to *"Add a Redis caching layer for the LangGraph state machine."*

1.  **Preflight (Where/Why)**: The agent verifies it's operating in WSL. It triggers `.venv/bin/python` to check the environment. If it matches, it proceeds.
2.  **Discovery (How - Phase 1)**: The agent calls `liet-ke-files` to identify the state manager file and `thiet-ke-luong-ai-va-multi-agent` to design how the cache integrates with the existing Multi-Agent contract.
3.  **Security & Sync (When/How - Phase 2)**: Before importing `redis-py`, the agent calls `scan_dependencies` to validate the package version. It uses `determine-threat-model` to identify that Redis lacks TLS by default, adding this risk to the `cap-nhat-checklist`.
4.  **Mutation (How - Phase 3)**: The agent uses `cap-nhat-codes` to write the Redis integration, explicitly forcing secure connection string handling as planned.
5.  **Verification (Where/How - Phase 4)**: The agent runs `kiem-tra-chat-luong-codes` inside the `var/tmp/codex/` sandbox to ensure unit tests pass, generating isolated cache files without polluting the Windows host.
