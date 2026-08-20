# AI Strategy One-Pager - Juno Automated Prioritization

## 1. Problem & Workflow

Juno prevents PMs from missing or silently deprioritizing a real P0 risk because it's buried in a backlog of thousands of open ROCKET tickets while the PM is heads-down elsewhere. Today that only gets caught when someone remembers to ask Juno to rank it — Automated Prioritization removes the "remembering" step

## 2. Target Metrics

Primary: Median time-to-rank — new P0/P1 signal landing in #escalations/#support-triage to appearing in a cited, ranked risk table — under 2 hours, measured over 30 days.
Trust guardrail metric: 100% of rows carry a valid Source ID (Slack link / Jira key / transcript timestamp); 0% invented fields.

## 3. Autonomy Level

Level: Assist. Juno proposes a ranked table; a human decides what to do with it. Explicitly not Agent — Juno will never autonomously re-order the backlog, close/modify a Jira ticket, or notify a customer based on its own ranking.

## 4. Data & Model Approach

Approach: Ground (RAG) over the four approved sources (Slack #escalations/#support-triage, Notion "RocketShip Product," Jira ROCKET, shared transcripts). Shortcut not taken: Refine (Fine-tune).

## 5. Risks & Mitigations

One-way-door risk: Once ranking runs continuously instead of on-demand, a PM may stop manually spot-checking it — so a single bad automated ranking (e.g., a real P0 scored low because only one thread had landed yet) could sit buried until it escalates into a contractual or support failure. Once that happens, rebuilding PM trust in the ranking is much harder than it was to earn the first time.
Guardrail: Keep the existing <70%-confidence handoff rule and "NEEDS CLARIFICATION" tagging active on every automated run, and add a hard floor: any thread newly tagged P0 is always surfaced in the next ranking pass regardless of its computed severity×frequency score — the automation can re-rank, but it can never fully suppress a P0.

## 6. V1 Scope

IN: Read-only, continuous monitoring of the four approved sources; produces a ranked risk table on a trigger/cadence, every row cited to a Source ID.
OUT (1): No autonomous writes — Juno never applies a Jira change, edits a Notion page, or sends a Slack message; a human always applies the change.
OUT (2): No churn/expansion risk ranking without ARR/usage data attached — if that data isn't in the source material, Juno asks for it rather than estimating.
OUT (3, bonus): No external-facing drafts (customer, prospect, press) — those route to the human PM.
