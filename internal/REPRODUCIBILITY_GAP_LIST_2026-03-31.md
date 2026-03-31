# Reproducibility Gap List

**Date:** 2026-03-31  
**Scope:** methods/protocol reproducibility from docs only  
**Reviewed docs:** `docs/METHODOLOGY.md`, `docs/EXPERIMENTAL_DESIGN.md`, `docs/HARDWARE_PAYLOAD.md`, `README.md`

---

## Executive result

Protocol architecture is strong, but there are remaining replication blockers for an external team reproducing the study without additional clarification.

Current status for this audit item: **completed with blockers identified**.

---

## Critical replication blockers

1. **Numeric lock artifacts missing**
   - Missing frozen numeric delta table per primary endpoint.
   - Missing frozen power table (sigma assumptions, n_required, n_planned).

2. **Uncertainty budget not numerically closed**
   - Multiple Type A/Type B contributors remain TBD in primary uncertainty budget.
   - Without closure, external replication cannot apply the same acceptance boundary.

3. **Synchronization acceptance thresholds incomplete**
   - Sync method and reporting are specified (PTP preferred, NTP fallback), but a strict pass/fail threshold for measured offset/jitter is not centralized as a hard gate.

## Major reproducibility gaps

1. **Execution package not fully frozen**
   - No single "analysis contract" file linking endpoint definitions, multiplicity correction map, and output table schema.

2. **Data schema and file contract not explicit enough**
   - Archival intent exists, but required folder/file naming conventions for all raw and processed artifacts are not fully formalized in one machine-checkable specification.

3. **Trajectory-option branch unresolved**
   - Session C T3 includes Option A vs Option B pending decision; reproducibility requires final branch lock (including seed/procedure if pseudo-random).

4. **Hardware weight verification still operationally pending**
   - Core sessions rely on estimated payloads until physical verification is finalized.

## Minor gaps

1. Centralized script version pinning/checksum manifest is not yet explicit.
2. A one-page "failure handling decision tree" for aborted/invalid blocks is not yet formalized.
3. Cross-doc pointers are good but could be reduced with one canonical protocol execution sheet.

---

## Recommended closure actions (in order)

1. Publish `delta_lock_table` + `power_lock_table` in a frozen internal file.
2. Publish finalized numeric uncertainty budget for primary endpoints.
3. Add sync pass/fail thresholds and decision rule (accept/re-run) as explicit protocol gate.
4. Freeze T3 option branch and seed policy.
5. Add a concise reproducibility execution manifest (inputs, outputs, filenames, script versions).

---

## Readiness interpretation

- For supervisor review: acceptable with clearly declared open items.
- For external reproducibility claim: **not yet complete** until critical blockers are closed.
