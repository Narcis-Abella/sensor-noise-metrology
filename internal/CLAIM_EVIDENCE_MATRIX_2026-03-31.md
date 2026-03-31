# Claim-to-Evidence Matrix (Truth Pass)

**Date:** 2026-03-31  
**Scope:** Active narrative claims after reference-truth repair  
**Decision policy:** keep / downgrade / retire based on directness of support

---

## 1) Core scientific claims

| Claim (literal, shortened) | Location | Supporting refs | Support type | Verdict | Action taken |
| --- | --- | --- | --- | --- | --- |
| TOST is the right inferential tool for sufficiency, not NHST | `README.md`, `METHODOLOGY.md`, `RESEARCH_PLAN.md` | [1], [2], [4], [5] | direct + contextual | keep | wording kept strong on logic, softened novelty language |
| Equivalent-testing framing exists in adjacent domains | `README.md`, `METHODOLOGY.md` | [4], [5], [6] | contextual | keep | [6] reframed as adjacent practical-equivalence, not direct robotics TOST precedent |
| First-in-robotics residual-level TOST application | `README.md`, `RESEARCH_PLAN.md` | [1]-[6], [57] | contextual | downgrade | changed to "to the best of our knowledge" / "early application" |
| Static AVAR is useful for IMU stochastic characterization | `README.md`, `RESEARCH_PLAN.md` | [9], [11], [14] | direct + indirect | keep | removed hard universal wording on fixed 10-12 h requirement |
| Fixed 10-12 h is required in all cases for RRW | `README.md`, `RESEARCH_PLAN.md` | [11] | weak/indirect | retire (hard form) | rewritten as conservative protocol choice, not universal law |
| Furrer proves datasheet values systematically underestimate operational drift | `README.md`, `RESEARCH_PLAN.md` | [10] | indirect | downgrade | recast as simulation-context precedent, not definitive proof claim |
| M4 thermal form is directly derived from [13] | `README.md` | [13] | indirect | downgrade | now stated as modeling choice informed by literature |
| Mid-360 kinematic-stress gap has limited direct prior evidence | `RESEARCH_PLAN.md`, `EXPERIMENTAL_DESIGN.md` | [26], [27] | indirect | keep | removed absolute "gap confirmed absent" phrasing |
| D455 thermal/FPN drift is directly proven by cited camera sources | `README.md` | [34], [37] | mixed (direct + analogical) | downgrade | now explicitly marked as partly analogical |
| Plugin gap: no standard CPU-first Humble/Fortress Rosetta path identified | `README.md`, `RESEARCH_PLAN.md` | [81], [82], [25] | contextual | keep | removed exclusivity ("only solution"/"incompatible") claims |
| Benchmarks (EuRoC/TUM-VI/etc.) prove pre-session AVAR protocol standard | `RESEARCH_PLAN.md` | [77], [78], [79], [80] | weak for AVAR-specific claim | retire (hard form) | kept as benchmark-quality context, removed AVAR-standard proof claim |
| Robot-arm references directly validate stochastic covariance identification | `RESEARCH_PLAN.md` | [40], [41], [42], [46], [47], [51] | mixed | downgrade | reframed as calibration/validation context, not direct stochastic-variance proof |

---

## 2) High-risk references triage (critical set)

| Ref | Status after repair | Keep/use mode | Notes |
| --- | --- | --- | --- |
| [6] | metadata corrected, interpretation softened | contextual | practical-equivalence adjacent evidence |
| [10] | reframed to sim-framework context | contextual | no longer used as strict AVAR-method authority |
| [11], [12], [13], [22], [23] | metadata/wording corrected | mixed (direct + contextual) | removed strongest overclaims; keep with bounded wording |
| [24], [26] | metadata corrected/softened | mixed | no absolute uniqueness claims |
| [34], [37] | metadata/DOI corrected and transfer caveated | contextual for D455 | no "same technology therefore direct proof" language |
| [41], [46], [47], [51], [54] | metadata corrected and scope tightened | contextual/mixed | no direct GT-equivalence overreach |
| [57], [60], [64] | bibliographic confidence heterogeneous | mostly contextual | [57] explicitly marked as HAL contextual record pending full normalization |
| [77], [78], [80] | claims corrected | contextual | removed AVAR-protocol overreach |
| [84], [87] | standards framing corrected | [84] contextual, [87] direct | [87] updated to 2023 edition; [84] no longer treated as MEMS-mandatory |

---

## 3) Readiness memo (go/no-go)

### Decision: **NO-GO (for supervisor submission today)**

Rationale:

1. Core narrative is now significantly safer, but a few citations still carry **contextual-only support** for claims that were previously central.
2. At least one reference ([57]) is intentionally retained as contextual record with non-final bibliographic normalization.
3. The reference corpus has been corrected in critical areas, but the full 88-entry list has not yet been revalidated line-by-line after these edits.

### Conditions to move to GO

- Final bibliographic normalization pass for all active-citation entries used in `README.md`, `METHODOLOGY.md`, and `RESEARCH_PLAN.md`.
- Zero unresolved "contextual-only" support for any claim presented as primary methodological justification.
- Quick final coherence pass to ensure every strengthened/softened claim is consistent across all active docs.

---

## 4) Integrity statement

This matrix follows a truth-first policy: claims were reduced whenever evidence was indirect, ambiguous, or mismatched, even if that lowered novelty strength.
