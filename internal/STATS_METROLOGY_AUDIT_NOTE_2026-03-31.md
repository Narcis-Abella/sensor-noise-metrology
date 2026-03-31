# Statistical and Metrology Audit Note

**Date:** 2026-03-31  
**Scope reviewed:** `README.md`, `docs/METHODOLOGY.md`, `docs/RESEARCH_PLAN.md`, `docs/EXPERIMENTAL_DESIGN.md`, `docs/HARDWARE_PAYLOAD.md`  
**Goal:** publication defensibility for IEEE TIM / Measurement style review

---

## Verdict summary

- TOST logic is conceptually correct and consistently framed.
- Endpoint hierarchy is present but still not fully operationalized for analysis-ready execution.
- Power and uncertainty framing are partially defined; critical numerical lock points remain pending.

Current status for this audit item: **completed with findings**.

---

## Checklist (Phase 7 criteria)

## 1) TOST formulation and interpretation

**Status:** PASS  

Evidence:

- Correct two one-sided null framing.
- Correct 90% CI equivalence criterion.
- Correct emphasis on pre-specified margin and non-post-hoc definition.

Residual risk: low.

## 2) Margin definition governance and pre-specification consistency

**Status:** PARTIAL  

Evidence:

- Unit-level delta definitions are present.
- Pre-specification intent is explicit across docs.

Gap:

- Fully locked numeric delta values per sensor endpoint are not yet visible as a final immutable table ready for execution.

Risk: medium-high for publication defensibility if execution starts before numeric lock.

## 3) Endpoint hierarchy and multiplicity handling

**Status:** PARTIAL  

Evidence:

- Primary endpoint (T2) and exploratory endpoints (T1/T3, CW/CCW) are declared.
- Holm-Bonferroni intent is stated.

Gap:

- A final endpoint registry (exact test family, exact corrected alpha allocation, exact reporting template) is not yet packaged as an execution artifact.

Risk: medium.

## 4) Power and sample-size logic consistency

**Status:** PARTIAL  

Evidence:

- Exact-TOST power reference and target (1-beta >= 0.80) are declared.
- Session structure suggests plausible repetition counts.

Gap:

- No finalized per-endpoint power table with explicit assumptions (sigma source, delta value, n_required, n_planned).

Risk: high if interpreted as pre-registered without finalized table.

## 5) Uncertainty budget consistency with metrology language

**Status:** PARTIAL  

Evidence:

- Type A / Type B framing is correctly used.
- RP/RT/AT distinction is now consistent in active docs.

Gap:

- Several budget entries remain TBD (fixture tolerances, probing repeatability, optional instrument terms).

Risk: high for external submission until numeric closure.

## 6) Traceability and limitation statements alignment

**Status:** PASS-PARTIAL  

Evidence:

- Limitations are explicitly declared and generally aligned with evidence.
- Claims were downgraded where support was contextual.

Gap:

- Some execution-critical traceability fields are described narratively but not yet centralized in a single analysis-ready metadata schema.

Risk: medium.

---

## Must-fix list before external manuscript submission

1. Lock numeric delta values per primary endpoint in a frozen table.
2. Freeze per-endpoint power table with explicit assumptions and calculations.
3. Close all TBD uncertainty-budget entries needed for primary conclusions.
4. Publish final endpoint/multiplicity registry used in analysis scripts.

---

## Readiness interpretation

- For supervisor discussion: acceptable with bounded risk.
- For external manuscript submission: **not yet defensible** until must-fix items above are closed.
