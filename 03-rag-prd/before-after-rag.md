## Diagnostic Diff · Juno RAG Lab

_Working notes from Module 3 Lab 1. Do not paste over `03-rag-prd/prd.md`. That file comes from the AI PRD Builder._

**Lovable prototype:** https://juno-pm-assist.lovable.app/

### Before - Quality Mode (no strategy)

CSV export crash / no error message — P1. Clear problem, direct user evidence ("I've lost hours"), specific and reproducible.
Nav bar color too bright — P2. Real user complaint with evidence, but subjective/low specificity.
Dark mode request — P2/P3. Vague, low specificity, closer to a "nice to have" than a defined requirement.

### After - Strategy Mode (with RocketShip Strategy One-Pager)

CSV export crash — P0, cited against "Reliability First" (the doc names CSV export crashes explicitly as a cause of lost enterprise deals).
Nav bar color change — notRecommended, cited against "What We Are NOT Doing" (aesthetic refresh).
Dark mode — notRecommended, cited against "What We Are NOT Doing" (aesthetic refresh).

### Takeaway

> Without a strategy document, Juno can only judge how well a request is written — not whether it matters; with one, it stopped treating 'this hurts my eyes' and 'my export loses data' as equally important"

