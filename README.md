# Juno — AI Associate PM for RocketShip's Escalation Pipeline

> Juno turns thousands of scattered P0/P1 signals into a cited, PM-reviewed top-5 risk list — automatically, the moment a thread crosses the danger threshold, never without a human sign-off

_Jaret + ai-product-management-aug17-26-weeknights_

Repo: https://github.com/yangz1986/juno-pm

This repo is my final project for the AI Product Management Certification — **Juno**. Each module’s artefact lives in its own folder; this README is the dashboard and the pitch.

---

## Module artefacts

### M1 · Prompting
- **System prompt** — [`01-prompting/system-prompt.md`](01-prompting/system-prompt.md)
- **Prototype** — https://juno-pm-assist.lovable.app

### M2 · Strategy
- **Decision matrix** — [`02-strategy/decision-matrix.md`](02-strategy/decision-matrix.md)
- **AI Strategy one-pager** — [`02-strategy/strategy-one-pager.md`](02-strategy/strategy-one-pager.md)

### M3 · RAG / AI PRD
- **AI PRD** — [`03-rag-prd/ai-prd.md`](03-rag-prd/ai-prd.md)

### M4 · AI-Native UX
- **AI user flow** — [`04-ai-ux/user-flow.md`](04-ai-ux/user-flow.md)
- **Trust-gap mitigations** — [`04-ai-ux/trust-gaps.md`](04-ai-ux/trust-gaps.md)

### M5 · Agentic Workflows
- **Agent Workflow Spec (AWSpec)** — [`05-agentic-workflows/awspec.md`](05-agentic-workflows/awspec.md)
- **Agent Control Panel** — [`05-agentic-workflows/agent-control-panel.md`](05-agentic-workflows/agent-control-panel.md)

### M6 · Evals &amp; Guardrails
- **Eval stack** — [`06-evals/eval-stack.md`](06-evals/eval-stack.md)
- **Human evaluation rubric** — [`06-evals/human-rubric.md`](06-evals/human-rubric.md)

---

## PM Execution Plan

### Where Juno is today
Juno today drafts on-demand ranked risk tables — Suggest/Assist autonomy, grounded in RAG over four approved sources, citing a Source ID on every row, with a <70%-confidence handoff already enforced. The Automated Prioritization bet — moving from pull-based to threshold-triggered ranking — is fully spec'd end to end (PRD → user flow → AWSpec → Control Panel → eval stack) but not yet shipped. It's ready for an engineering build, not a live feature yet.

### What ships next (next 2 sprints)
- Sprint 1: ship the threshold trigger (5 messages/10 min on a P0/P1 tag) and the Modular RAG pipeline (Top-K=15, hybrid retrieval, p95≤4s), behind a feature flag, posting only to the PM review queue — no auto-post anywhere. 
- Sprint 2: ship the kill switch (demote / needs-human-review buttons), wire it into the eval stack's Layer A feedback signal, and run the first weekly human-eval batch (40 runs) against the golden set before removing the flag.

### What I watch (dashboards)
- Time-to-rank (target <2h), 
- the four M4 trust-gap scores, 
- the weekly human-eval pass rate (≥4.0/5 mean, 0 critical safety fails), 
- the automated CI checks (format / citation / refusal / scope), and demote rate broken out per recurring theme

### Red lines (what blocks shipping)
Any scope-boundary violation — a call to Salesforce or any source outside the four approved ones — hard-blocks the build, no exceptions. A citation-check failure on the golden set hard-blocks. p95 latency >4s requires my sign-off before shipping. Human-eval mean <4.0/5 on Accuracy or Safety for 2 consecutive weekly batches rolls the feature flag back to on-demand-only. Cost per run >$0.50 (Top-K=15 retrieval + LLM-judge pass) requires my sign-off before scaling past the pilot cohort.

### Governance
- Compliance: PII redaction and the never-invent rule are the closest controls we have today; RocketShip's actual GDPR/EU AI Act exposure was never addressed in any of my source material, so I'm flagging that as an open question for legal, not something I've solved.
- Safety: never invent ARR/PII/customer names; tool access is hard-scoped to four read sources with no autonomous write, closing off the main prompt-injection/misuse surface.
- Reliability: max 6 steps and an 8-second timeout per run, abort after 2 tool errors, degrade to "evidence-only mode" (raw links, no computed rank) rather than fail silently.
- Reputation: Juno never drafts or sends anything for external audiences — that's a flat rule from day one — so the worst public-failure scenario (a fabricated ranking reaching a customer) is structurally blocked rather than merely discouraged; any internal miss gets caught by the demote signal and reviewed at the next weekly batch.

---

## Build Insights

- **Friction point.** The hardest part for me wasn't the UX tools — it was realizing that almost every real constraint I hit (Salesforce being out of scope, Jira writes needing to stay human-gated) came from re-reading the system prompt's guardrails, not from anything in the M2–M5 tools themselves. I had to keep going back to a document I wrote in Module 1 to check whether a Module 5 default was actually allowed
- **Key learning.** Autonomy level isn't a UX preference, it's downstream of what your product already promised in its rules. I kept being tempted to reach for "Agent" because the course's own worked examples used it — but my own system prompt had already ruled that out in M3 modules, and I almost missed the contradiction
- **Aha moment.** The trust-gap scores from M4 and the hard-block gates from M6 turned out to be checking the same three things — citation, confidence, control — just at two different points in the pipeline: one at design time, one at runtime. That's the moment the whole course stopped feeling like six separate exercises and started feeling like one system.

---

_Certification submission — AI Product Management Certification._
