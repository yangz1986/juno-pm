# AI Solution Decision Matrix · Juno

## The decision

How do we implement continuous, automated risk ranking for Juno, now that on-demand ranking (Suggest-level) has proven the mechanic works and the PM no longer needs to manually re-verify it every time?

## Options scored

| Option | Cost | Speed | Control | Moat | Risk | Score |
|---|---|---|---|---|---|---|
| Build | 3 | 3 | 5 | 4 | 4 | 3.8 |
| Buy / API | 4 | 5 | 2 | 1 | 2 | 2.8 |
| Fine-tune | 1 | 1 | 3 | 3 | 2 | 2.0 |

## Recommendation

It scores highest overall (3.8 vs. 2.8 vs. 2), and more importantly it's the only option that inherits Juno's existing guardrails (source citation, confidence-threshold handoff, no autonomous sends) instead of requiring RocketShip to re-negotiate them with a vendor or retrain them into a fine-tuned model. Since Automated Prioritization is a cadence change to a pillar that already exists and is scoped at Suggest, extending the current build is lower-risk than introducing a new system with a different trust surface.
