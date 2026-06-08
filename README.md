# Career Intelligence Platform

Instead of hopping between job portals to hunt for roles, **Career Intelligence Platform** is a personal platform that brings the *right* roles to you — the ones that genuinely fit, whether you're ready for them today or aiming to transition into them next. And it sharpens over time: by learning from your career progress, it builds an evolving **career DNA** that drives better role suggestions and more targeted preparation at every step.

| | |
|---|---|
| 🎬 **Live walkthrough** | https://ragkv.github.io/portfolio/ |
| 💻 **Source code** | https://github.com/ragkv/Career-Intelligence-Platform *(currently private — see below)* |
| 👤 **Built by** | Raghava Kundavajjala |

> 🔐 **Source access** — the code repository may be **private** while the project is being prepared for public release, so the link above can return a 404. If you'd like to review the source (e.g. for hiring or collaboration), I'm glad to grant read access on request — [open an issue](https://github.com/ragkv/portfolio/issues) and I'll add you as a collaborator.

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
