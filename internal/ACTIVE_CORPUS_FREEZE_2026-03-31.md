# Active Authoritative Corpus Freeze - 2026-03-31

**Purpose:** Freeze the active source-of-truth corpus and terminology policy before deep technical and editorial review.

**Effective date:** 2026-03-31
**Status:** Active baseline for Q1 audit cycle
**Owner:** Narcis Abella

---

## 1) Active authoritative files (frozen baseline)

The following files are the only authoritative set for deep review in this cycle:

1. `README.md`
2. `docs/RESEARCH_PLAN.md`
3. `docs/METHODOLOGY.md`
4. `docs/EXPERIMENTAL_DESIGN.md`
5. `docs/HARDWARE_PAYLOAD.md`
6. `docs/REFERENCES_CONSOLIDATED.md`
7. `PROGRESS_LOG.md`

Any coherence, citation, or scope finding must be evaluated against this set only.

---

## 2) Archive boundary policy

- Files under `archived/` are non-authoritative context.
- Deprecated files replaced by consolidated references are non-authoritative context:
  - `docs/EXTENDED_LITERATURE_REVIEW.md`
  - `docs/REFERENCES_POOL.md`
  - `docs/SLAM_BACKENDS.md` (moved to `archived/`)
- Archived/deprecated material may be used for historical traceability only and must not be treated as current scope definition.

---

## 3) Terminology policy (locked for this review cycle)

### 3.1 Scope language

- Canonical study framing: metrological characterization of robotic sensor noise models and residual-level equivalence validation.
- "SLAM" can appear only as downstream context, motivation, or future extension.
- SLAM backend benchmarking is not an active objective in this corpus.

### 3.2 Stage naming

- Use "Stage 1" and "Stage 2" for internal operational structure of the current experiment.
  - Stage 1: static characterization
  - Stage 2: dynamic sessions A-D
- Do not use legacy macro-study phase framing (for example, old three-phase proposal wording) as active terminology.

### 3.3 Claim discipline

- Distinguish clearly between:
  - evidence-supported claims
  - planned protocol elements
  - future work extensions
- Keep novelty language conservative and bounded to currently defensible claims.

---

## 4) Usage rule for reviewers

During the deep review, if any statement conflicts with this freeze note, this document and the active authoritative file set above take precedence.
