# Final Fix Queue and Readiness Recommendation

**Date:** 2026-03-31  
**Basis:** reference truth pass + submission hardening + stats/metrology audit + reproducibility gap audit

---

## Prioritized fix queue

## Critical (blocks external manuscript submission)

1. **Freeze numeric delta values** per primary endpoint in a final locked table.
2. **Freeze power assumptions and required n** per primary endpoint (explicit sigma source and formula output).
3. **Numerically close uncertainty budget** for all contributors used in primary claims (remove critical TBDs).
4. **Publish strict endpoint registry** (primary vs exploratory + multiplicity correction map).

## Major (should be closed before declaring fully reproducible package)

1. Freeze Session C T3 branch (Option A vs B) and seed policy.
2. Add explicit synchronization pass/fail threshold for measured offset/jitter.
3. Finalize a unified data/filename contract for raw, intermediate, and output artifacts.
4. Complete physical payload verification and publish measured values for core sessions.

## Minor (quality hardening, not immediate blockers)

1. Add compact failure-handling decision tree for invalid blocks.
2. Add script/version manifest with checksum-style traceability.
3. Add one-page "analysis runbook" that points to all frozen lock tables.

---

## Final readiness recommendation

### For supervisor review meeting: **GO (bounded risk)**

Reason:

- Core scientific narrative is now conservative and internally coherent.
- Citation/claim overreach risk has been materially reduced.
- Remaining issues are mostly execution-freeze artifacts, not conceptual validity blockers.

### For external manuscript submission: **NO-GO (until critical fixes are closed)**

Reason:

- Critical lock artifacts (delta/power/uncertainty closure) are still not fully frozen in final form.
- External reviewers can still challenge defensibility on pre-specification and uncertainty closure grounds.

---

## Stop criteria to switch external NO-GO -> GO

All must be true:

1. Zero critical items open.
2. Major items either closed or explicitly bounded in manuscript limitations.
3. No unresolved claim in core contribution sections depends only on weak contextual support.
4. Final consistency pass confirms no citation index drift in active docs.
