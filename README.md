# Career Intelligence Platform

A **local-first, evidence-grounded career-intelligence engine** — upload a résumé, paste a job description, and get an honest, *cited* skill-gap report in seconds, without your résumé ever leaving your machine.

| | |
|---|---|
| 🎬 **Live walkthrough** | https://ragkv.github.io/portfolio/ |
| 💻 **Source code** | https://github.com/ragkv/Career-Intelligence-Platform |
| 👤 **Built by** | Raghava Kundavajjala |

---

## What it does
Upload a résumé PDF + a job description → the platform parses the résumé with a **local** LLM, scores every required skill against real evidence from your career history, and produces a prioritised, week-by-week learning plan. A separate **Mutation Agent** rewrites résumé bullets to surface transferable experience — bounded by what actually exists in your profile, never invented.

## What makes it interesting — the engineering
- **🔒 Sensitivity-aware LLM router (ADR-007)** — résumé & career data are routed to on-device **Ollama only**, in *every* mode; only de-identified, public data (job descriptions, skill names) is ever eligible for a cloud model.
- **🚫 Evidence before score** — Pydantic validates every LLM output; a skill with **no cited evidence is forced to 0**. Hallucination blocked by design.
- **⚖️ Two-model verification** — critical, low-confidence gaps are independently re-checked by a second model (Sonnet → Haiku → GPT-4o → Ollama); the final score is the consensus of scorer + verifier.
- **🏛️ Six-layer clean architecture** — `frontend → api → services → repositories/agents → domain`, strict one-way dependencies, each layer tested in isolation.
- **💰 Cost-governed** — a hard monthly budget cap is checked before every paid call; on the cap, calls fall back to local Ollama so analysis never fails. Runs at **~$0–$1/month**.
- **💾 Crash-safe persistence** — every write is temp-file → fsync → atomic rename. **280 tests**, fully mocked (no keys or Ollama needed in CI).

## Stack
Python 3.14 · FastAPI · LangGraph · Ollama / Claude / OpenAI · Pydantic · PostgreSQL + pgvector · Vanilla JS (no build step)

## Explore this portfolio
- 🎬 **[Animated system design](https://ragkv.github.io/portfolio/)** — a live trace of one `/analyze` request through all six layers
- 📐 **[Architecture diagram](architecture.html)**
- 📋 **[Case study](case-study.html)** — screens + engineering notes
- 🧪 **[Demos](demos.html)**

---

*Built by Raghava Kundavajjala.*
