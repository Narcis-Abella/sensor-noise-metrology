# Context Document for Repository Rewrite
**Date:** 2026-03-28  
**Purpose:** Briefing for Claude Code to rewrite the repository documentation  
**Source:** Extended research and strategy session (Claude.ai)

---

## 1. Critical scope change — the most important thing

**The study scope has shifted completely away from SLAM.**

The previous README and all docs framed this as a SLAM validation study that happens to characterize sensors. That framing is wrong and must be replaced.

**New framing:**
> This is a metrological characterization study of robotic sensor noise models for simulation. The primary question is: can we formally demonstrate — using statistical equivalence testing (TOST) with pre-specified margins — that a metrologically-derived sensor noise model in simulation is statistically equivalent to real hardware at the signal level?

**SLAM is mentioned only as one downstream application**, not as the scope or target. One or two sentences max, framed as: "The resulting noise models are designed to be injected into simulation plugins (e.g. Gazebo Fortress), enabling downstream use cases such as SLAM algorithm evaluation without requiring repeated hardware sessions."

**Why this matters for the rewrite:**
- The metric of equivalence is NOT ATE/RPE (those are SLAM metrics)
- The metrics are direct sensor residuals: point-to-plane residuals (LiDAR), IMU residuals against YuMi kinematic ground truth, camera pose drift of static AprilTag board
- FAST-LIO2, GLIM, ORB-SLAM3 etc. can stay in SLAM_BACKENDS.md as a planned extension but must not appear in the core claims or abstract-level framing

---

## 2. What the study actually does (new scope, clean version)

1. **Static characterization** — sensors fixed, immobile:
   - IMUs: 10–12h logs → Allan Variance (ARW, BI, RRW) + Six-Position Test (IEEE Std 1293)
   - LiDAR: planar orthogonal residual method (point-to-plane residuals vs. reference plane at t=0) → thermal ToF drift
   - Camera (D455): AprilTag board static for 3–4h → thermal intrinsic drift + FPN

2. **Dynamic characterization** — sensors on ABB YuMi arm:
   - YuMi provides kinematic ground truth (path repeatability RT = 0.10 mm, path accuracy AT = 1.36 mm)
   - Four sessions A–D, one sensor per session
   - Residuals computed: measured − true (YuMi-derived) for each sensor
   - Noise model M1→M4 hierarchy fitted from residuals

3. **Equivalence validation (TOST)**:
   - Compare distributions of sensor residuals: real hardware vs. simulated (M1→M4)
   - TOST with pre-specified margin δ (defined before data collection, NOT post-hoc)
   - If 90% CI for mean difference lies within [−δ, +δ]: equivalence declared
   - This is applied at the SENSOR SIGNAL level, not at the SLAM trajectory level

4. **Software deliverable**: Gazebo Fortress plugin for Livox Mid-360 Rosetta pattern with M4 noise injection (no existing ROS 2 Humble compatible solution exists)

---

## 3. The noise model hierarchy (M1→M4) — unchanged

| ID | Name | Source |
|----|------|--------|
| M1 | Manufacturer | Datasheet / community defaults |
| M2 | Static Allan | Long static logs (10–12h) |
| M3 | In-Session Static | 60s static windows within dynamic sessions |
| M4 | Kinematic-Residual + Thermal | State-dependent: f(T, v, ω, a, ω̇, ȧ) fitted from YuMi residuals |

M4 is NOT the primary contribution. It is a necessary enabler so the TOST has sufficient resolution. The primary contribution is the TOST-based equivalence framework applied to sensor noise model validation — confirmed as a literature gap.

---

## 4. Confirmed literature gaps (verified in this session)

These are the novelty claims, confirmed by exhaustive search:

**Gap 1 (Primary — TOST):**  
No prior work applies TOST to sensor noise model validation for simulation. The three closest analogues are:
- Robinson et al. 2005 (*Ecological Modelling*) — TOST for model validation in general (ecology)
- Ramert, AFIT STAT COE 2020 — TOST for M&S validation in defense (system-level outputs, not sensor signals). Literally states: "Model validation is an ideal application for equivalence testing."
- Wu et al. arXiv:2505.12827 (2025) — TOST for synthetic ADAS scenario validation

None of these apply TOST at the sensor residual level. This is the primary novelty.

**Gap 2 (ICM-40609):**  
No independent published characterization of the TDK InvenSense ICM-40609 (the IMU inside the Livox Mid-360) exists in the literature. Only the TDK datasheet provides specs. The study's Allan Variance characterization is therefore an original contribution.

**Gap 3 (Hand-eye → ATE/RPE propagation):**  
While hand-eye calibration methods are well-studied (Tsai-Lenz, Park-Martin, Daniilidis), no work systematically quantifies how hand-eye calibration uncertainty propagates into trajectory evaluation metrics. Typical residuals: ~0.2–1 mm translation, ~0.1–0.3° rotation.

**Gap 4 (Mid-360 vibration characterization):**  
No experimental characterization of Livox Mid-360 range noise under mechanical vibration/kinematic stress exists. Schlager 2021 tested Ouster only; Brazeal 2021 simulated Risley prism misalignment without experimental validation.

**Gap 5 (Fortress plugin):**  
No ROS 2 Humble / Gazebo Fortress plugin for the Mid-360 Rosetta pattern exists. All prior plugins target Gazebo Classic (EOL Jan 2025) or require NVIDIA OptiX/CUDA (RobotecAI, targets Harmonic).

---

## 5. New references to add to the pool

These are verified and not currently in REFERENCES_POOL.md or RESEARCH_PLAN §9. Add them to the consolidated references doc.

### Must-add (directly citable in paper):

**[NEW-01]** A. Ramert, "Equivalence Testing," STAT COE Best Practice Report 12-2020, Air Force Institute of Technology (AFIT), 2020.  
URL: https://www.afit.edu/STAT/statcoe_files/1005AFIT2020ENS09117%201005rame%202-2.pdf  
*Topic: TOST in engineering/defense M&S validation. Confirms "model validation is an ideal application for equivalence testing." Cites weapon shot sim vs. real as example.*

**[NEW-02]** C. M. Robinson, "Model validation using equivalence tests," *Ecological Modelling*, vol. 176, no. 3–4, pp. 349–358, 2004. DOI: 10.1016/S0304-3800(04)00098-5  
URL: https://www.sciencedirect.com/science/article/pii/S0304380004000985  
*Topic: First paper proposing TOST for model validation. Argues that classical NHST has the null hypothesis backwards for model validation — the burden of proof should be on the model to prove equivalence. Directly supports the methodological argument.*

**[NEW-03]** N. El-Sheimy, H. Hou, and X. Niu, "Analysis and Modeling of Inertial Sensors Using Allan Variance," *IEEE Trans. Instrumentation and Measurement*, vol. 57, no. 1, pp. 140–149, 2008. DOI: 10.1109/TIM.2007.908635  
*Topic: Seminal paper (750+ citations) on Allan variance for IMU characterization. More widely cited than Furrer 2016 for this specific topic. Essential for IEEE TIM submission.*

**[NEW-04]** E. Olson, "A Passive Solution to the Sensor Synchronization Problem," *Proc. IEEE/RSJ IROS*, pp. 1059–1064, 2010. DOI: 10.1109/IROS.2010.5650579  
*Topic: Quantifies that 10 ms sync error at 90°/s causes 15.7 cm projection error. The concrete number for justifying PTP over NTP in the experimental protocol.*

**[NEW-05]** I. Enebuse, M. Foo et al., "Accuracy Evaluation of Hand-Eye Calibration Techniques for Vision-Guided Robots," *PLoS ONE*, vol. 17, no. 10, e0273261, 2022. DOI: 10.1371/journal.pone.0273261  
*Topic: Quantitative comparison of 6 AX=XB algorithms on real robot. Reports numerical residuals under varying noise. Justifies the ≥30 poses protocol and expected error range.*

**[NEW-06]** S. Liu et al., "A Spatiotemporal Hand-Eye Calibration for Trajectory Alignment in Visual(-Inertial) Odometry Evaluation," arXiv:2404.14894, 2024.  
*Topic: Hand-eye calibration specifically in the context of sensor evaluation against MoCap/robot ground truth — the only paper that directly parallels the study's use case.*

**[NEW-07]** G. Shieh, "Exact Power and Sample Size Calculations for the Two One-Sided Tests of Equivalence," *PLoS ONE*, vol. 11, no. 9, e0162093, 2016. DOI: 10.1371/journal.pone.0162093  
*Topic: Exact (not approximate) power functions and sample size formulas for TOST. Resolves the P0 item in PENDING_2026-03-27.md about formal power analysis before YuMi booking.*

### Should-add (methodology support):

**[NEW-08]** S. B. Gundersen and E. Halvorsen, "The Syncline Model — Analyzing the Impact of Time Synchronization in Sensor Fusion for Robotic Applications," arXiv:2209.01136, 2022.  
*Topic: Analytical model of sync error impact in sensor fusion. Complements Olson 2010.*

**[NEW-09]** M. Faizullin, A. Kornilova, and G. Ferrer, "Open-Source LiDAR Time Synchronization System by Mimicking GNSS-Clock," arXiv:2107.02625, 2021.  
*Topic: MCU-based LiDAR-IMU sync achieving 1 µs precision. Directly relevant to Mid-360 sync protocol.*

**[NEW-10]** G. Yan et al., "Effective Bias Warm-Up Time Reduction for MEMS Gyroscopes Based on Active Suppression of the Coupling Stiffness," *Microsystems & Nanoengineering*, vol. 5, art. 18, 2019. DOI: 10.1038/s41378-019-0057-2  
*Topic: MEMS gyro warm-up ~2000 s without compensation. Quantitative physical justification for the 20-minute warm-up protocol of Mid-360.*

**[NEW-11]** S. A. Pardo, *Equivalence and Noninferiority Tests for Quality, Manufacturing and Test Engineers*, CRC Press, 2014. ISBN: 978-1466586888.  
*Topic: The only textbook on equivalence testing for engineers (not pharma). Useful for framing TOST as "methodology well-established outside robotics" in IEEE TIM.*

---

## 6. Hand-eye calibration — conceptual summary (for README and docs)

Hand-eye calibration solves for the rigid transform X between the robot flange and the sensor's optical/inertial center. Without it, all trajectory comparisons have a systematic offset equal to the mounting geometry.

The AX=XB equation: A = flange motion (from RobotStudio), B = sensor-observed motion, X = unknown flange-to-sensor transform.

**Verification protocol** (already in EXPERIMENTAL_DESIGN §10, keep as-is):  
Move YuMi to a fixed verification pose. Sensor observes the static AprilTag board. Predicted vs. observed pose is compared. Acceptance criterion: <1 mm translation, <0.5° rotation reprojection error. If fails: remount and redo AX=XB.

**Expected residuals from literature (Enebuse 2022):** ~0.2–1 mm translation, ~0.1–0.3° rotation. These enter the GUM uncertainty budget in METHODOLOGY §2.4.

---

## 7. Temporal synchronization — key numbers for docs

| Method | Accuracy |
|--------|----------|
| PTP IEEE 1588 | <1 µs |
| GNSS-mimicking (Faizullin 2021) | ~1 µs |
| NTP well-configured | ~0.2 ms |
| ROS 2 software timestamps | >1 ms jitter |
| ABB EGM cycle | 4 ms |
| **Impact: 10 ms @ 90°/s** | **15.7 cm error (Olson 2010)** |

PTP is the preferred method. NTP is fallback with documented jitter. The spatial error from timing uncertainty must be included in the uncertainty budget.

---

## 8. Instructions for the README rewrite

**Structure the new README around these sections:**

0. **Why this study matters** — Lead with the metrological argument: sensor models in simulation are never validated rigorously; domain randomisation fails because it doesn't fix structurally wrong noise statistics; TOST provides the missing statistical framework. SLAM mentioned only as one downstream application.

1. **What this project is** — Metrological characterization of sensor noise models. Ground truth: ABB YuMi (RT = 0.10 mm). Sensors: IMU, LiDAR, RGB-D. Goal: TOST-based equivalence between real and simulated sensor residuals.

2. **Scope** — Sensor characterization only. Not a SLAM benchmark. Future work only for SLAM evaluation.

3. **Hardware** — Same table as current, unchanged.

4. **Experimental design** — Static + dynamic, same as current but with residuals (not ATE/RPE) as the primary outcome.

5. **Noise models M1–M4** — Same as current, emphasize M4 as enabler not primary contribution.

6. **TOST equivalence framework** — Primary contribution. Explain the flip in burden of proof vs. classical NHST. Cite Robinson 2005, Ramert 2020, Wu 2025 as analogues in other domains.

7. **Software contribution** — Gazebo Fortress plugin for Mid-360 Rosetta pattern.

8. **How to read the repository** — Same structure as current.

9. **Timeline** — Same as current.

10. **Known limitations** — Same as current.

**Tone:** Direct, metrological, no hedging. Every claim either cited or declared as study contribution.

---

## 9. What NOT to change

- The session structure A–D (IMU-only → 2D LiDAR → 3D LiDAR → visual-inertial)
- The M1→M4 noise model hierarchy and formulas
- The TOST procedure (METHODOLOGY §3.4) — this is already correct
- The uncertainty budget structure (METHODOLOGY §2.4)
- The experimental protocol (EXPERIMENTAL_DESIGN.md) — keep as-is
- SLAM_BACKENDS.md — keep but clearly label as "planned extension, not current scope"
- The PROGRESS_LOG.md structure
- The GitHub repo name: slam-sensor-metrological-validation (historical, keep for continuity)

---

## 10. Consolidated references document

Create a new file `docs/REFERENCES_CONSOLIDATED.md` that:
- Merges RESEARCH_PLAN §9 ([1]–[48]) + REFERENCES_POOL.md + EXTENDED_LITERATURE_REVIEW.md + the new references [NEW-01]–[NEW-11] from this document
- Assigns sequential numbers to all references
- Tags each with topics: [TOST] [AVAR] [HAND-EYE] [SYNC] [LIDAR] [IMU] [CAMERA] [SLAM] [METROLOGY] [SIM2REAL]
- Removes duplicates (several appear in both RESEARCH_PLAN §9 and REFERENCES_POOL)
- This becomes the single source of truth for all citations across all docs

---

*End of context document. Pass this to Claude Code along with the full repository.*