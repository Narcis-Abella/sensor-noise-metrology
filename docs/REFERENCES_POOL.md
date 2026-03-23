# References Pool — Phase I (for later use)

> **Purpose:** Dense list of additional references identified during the Phase I literature sweep (March 2026). Use when drafting the manuscript, when facing a specific experimental problem, or when a reviewer asks for support. Each entry has a short note on **why it may interest you**.  
> **Status:** Not all are cited in RESEARCH_PLAN.md; pick as needed. References [40]–[48] are already cited in RESEARCH_PLAN.md §9. References [49]–[63] added after adversarial novelty audit (2026-03-23).

---

## 1. Allan Variance, IMU noise modelling, Kalman/process noise

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 1 | **Z. Miao et al.**, "Online Estimation of Allan Variance Coefficients Based on a Neural-Extended Kalman Filter," *Sensors* 15(2):2496–2524, 2015. [MDPI](https://www.mdpi.com/1424-8220/15/2/2496) | Extends AVAR to online estimation of coefficients; useful if you discuss adaptive or in-session refinement of M2/M3. |
| 2 | **K. A. Lethander & C. N. Taylor**, "Conservative Estimation of Inertial Sensor Errors Using Allan Variance Data," *NAVIGATION* 70(3), navi.563, 2023. [ION](https://navi.ion.org/content/70/3/navi.563) | Derives conservative error bounds from AVAR; directly supports your ground-truth uncertainty budget and reporting of confidence intervals. |
| 3 | **Sliding Average Allan Variance for Inertial Sensor Stochastic Error Analysis**, IEEE. [Xplore](https://ieeexplore.ieee.org/document/6576229) | Alternative AVAR estimator (sliding/windowed); useful if you compare estimators or discuss robustness of M2/M3 extraction. |
| 4 | **DaischSensor**, "How Can Allan Variance Analysis Be Used to Model IMU Noise and Configure Kalman Filter Process Noise?" [Blog](https://daischsensor.com/how-can-allan-variance-analysis-be-used-to-model-imu-noise-and-configure-kalman-filter-process-noise/) | Plain-language link between AVAR coefficients and Kalman process noise; good for writing an intuitive Methods subsection or a tutorial-style appendix. |
| 5 | **Analysis of noise contributions in low-cost IMUs through Allan's variance**, IEEE Conf., 2025. [Xplore](https://ieeexplore.ieee.org/document/10189971) | Recent low-cost IMU AVAR study; useful when comparing your three IMU tiers (WT901C, BMI055, ICM40609). |
| 6 | **WaveLab SLAM 2017**, "IMU Noise and Characterization" (slides). [PDF](http://wavelab.uwaterloo.ca/slam/2017-SLAM/Lecture9-IMU_noise_characterization/IMU_Noise_and_Characterization.pdf) | Teaching material on PSD, AVAR, IMU noise model, preintegration; handy for structuring the Allan Variance section or for reviewer-friendly background. |
| 46 | **A. Solodar and I. Klein**, "VIO-DualProNet: Visual-inertial odometry with learning based process noise covariance," *Engineering Applications of Artificial Intelligence*, 2024. [DOI](https://www.sciencedirect.com/science/article/abs/pii/S0952197624006249) | State-dependent IMU covariance via dual DNN; 25% improvement over constant-covariance baseline. **Primary prior art for M4 concept** — cite in RESEARCH_PLAN §3.6 differentiation. Already in RESEARCH_PLAN §9 as [40]. |
| 47 | **S. Qiu et al.**, "AirIMU: Learning Uncertainty Propagation for Inertial Odometry," arXiv:2310.04874, 2023. [arXiv](https://arxiv.org/abs/2310.04874) | CNN-based per-frame covariance estimation for IMU integration. **Second primary prior art for M4 concept** alongside VIO-DualProNet. Already in RESEARCH_PLAN §9 as [41]. |

---

## 2. Ground truth, robot arm validation, metrology

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 7 | **L. Ricci, F. Taffoni, D. Formica**, "On the Orientation Error of IMU: Investigating Static and Dynamic Accuracy Targeting Human Motion," *PLOS ONE*, 2016. [PLOS](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0161940) | Separates static vs dynamic IMU accuracy with controlled motion; analogous to your Stage 1 vs Stage 2 and supports discussion of dynamic validation. |
| 8 | **F. Taffoni et al.**, "Validation of Novel Relative Orientation and Inertial Sensor-to-Segment Alignment Algorithms for Estimating 3D Hip Joint Angles," *Sensors* 19(23), 5143, 2019. [MDPI](https://www.mdpi.com/1424-8220/19/23/5143) | IMU validation against external reference and segment alignment; useful for hand–eye / segment calibration narrative. |
| 9 | **Z. Wan et al.**, "An Improved Design of the MultiCal On-Site Calibration Device for Industrial Robots," *Sensors* 23, 5717, 2023. [MDPI](https://www.mdpi.com/1424-8220/23/12/5717) | Metrology-grade calibration of industrial arms; supports discussion of YuMi as metrological tool and alternatives (laser tracker, calibration rigs). |
| 10 | **J. Kuti, T. Piricz, P. Galambos**, "A Robust Method for Validating Orientation Sensors Using a Robot Arm as a High-Precision Reference," *Sensors* 24(24), 8179, 2024. *(Already [10] in RESEARCH_PLAN.)* | Your core robot-arm validation reference; use for Related Work and Methods when describing YuMi-based orientation validation. |
| 48 | **C. Ferguson, T. Ertop, M. Herrell, and R. J. Webster III**, "Unified Robot and Inertial Sensor Self-Calibration," *Robotica*, vol. 41, no. 5, pp. 1590–1616, 2023. [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC10508886/) | Uses collaborative arm to estimate IMU intrinsic parameters from dynamic residuals via nonlinear least squares. **More direct precedent than Kuti for residual-based coefficient fitting.** Cite in RESEARCH_PLAN §3.5 alongside Kuti. Already in RESEARCH_PLAN §9 as [42]. |

---

## 3. Solid-state LiDAR, Livox Mid-360, characterisation

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 11 | **D. Mawuto Koudjo Felix et al.**, "Lidar Variability: A Novel Dataset and Comparative Study of Solid-State and Spinning Lidars," arXiv:2507.04321, 2025. [arXiv](https://arxiv.org/html/2507.04321v1) | Direct comparison solid-state vs spinning; supports your choice of Mid-360 and discussion of non-repetitive patterns vs LIO-SAM-style algorithms. |
| 12 | **"Mid360-based Lidar and IMU Tightly-coupled Odometry and Mapping,"** IEEE conf. [Xplore](https://ieeexplore.ieee.org/document/10011701) | Odometry/SLAM pipeline for Mid-360; cite when listing existing Mid-360 tight-coupling work alongside FAST-LIO2/GLIM. |
| 13 | **M. O. Mints et al.**, "Online Calibration of Extrinsic Parameters for Solid-State LIDAR Systems," *Sensors* 24(7), 2155, 2024. [PMC](https://pmc.ncbi.nlm.nih.gov/articles/PMC11014319/) | Online extrinsics for solid-state LiDAR; relevant if you run into LiDAR–IMU or LiDAR–flange drift during sessions. |
| 14 | **Y. Lo et al.**, "Performance Analysis of Low-Cost Solid-State LiDAR for Building Elements Point-Cloud Mapping," ICIMR 2024, Springer, 2025. [Springer](https://link.springer.com/chapter/10.1007/978-981-96-3949-6_25) | Accuracy/performance of low-cost solid-state LiDAR; supports cost/performance discussion of Mid-360 in HARDWARE_PAYLOAD. |
| 15 | **Livox-SDK/LIO-Livox**, "A Robust LiDAR-Inertial Odometry for Livox LiDARs," GitHub. [Repo](https://github.com/Livox-SDK/LIO-Livox) | Reference implementation for Livox LIO; useful for reproducibility and for comparing your backends (FAST-LIO2, Point-LIO, GLIM). |
| 16 | **Livox Tech**, "Livox Revolutionizes Smart Robotics with a Compact, Omnidirectional LiDAR Sensor Mid-360," 2023. [Newsroom](https://www.livoxtech.com/news/mid360_launch) | Manufacturer specs and positioning of Mid-360 (FOV, density, 360°); for Introduction or sensor selection justification. |
| 53 | **B. Vultaggio, F. Giacomini, and A. Vitti**, "Simulation of Low-Cost MEMS-LiDAR and Analysis of Its Effect on the Performances of State-of-the-Art SLAMs," *ISPRS Archives*, vol. XLVIII-1/W1-2023, pp. 539–546, 2023. [DOI](https://isprs-archives.copernicus.org/articles/XLVIII-1-W1-2023/539/2023/) | Built Mid-360 Gazebo Classic plugin with corrected scan pattern. Used to benchmark KISS-ICP, CT-ICP, LIO-SAM, FAST-LIO2 — all with generic Gaussian noise. **Primary prior art for the Fortress plugin gap** — cite in RESEARCH_PLAN §6.2. Already in RESEARCH_PLAN §9 as [44]. |
| 54 | **gazebosim/gz-sim**, "Custom lidar sensor — Feature Request," GitHub issue #1958, opened April 2023. [GitHub](https://github.com/gazebosim/gz-sim/issues/1958) | Community demand for Livox-style custom LiDAR in gz-sim since 2023, unresolved. **Evidence of the Fortress plugin gap.** Already in RESEARCH_PLAN §9 as [47]. |
| 55 | **RobotecAI/RGLGazeboPlugin**, GitHub. [GitHub](https://github.com/RobotecAI/RGLGazeboPlugin) | Only existing gz-sim plugin with Mid-360 Rosetta pattern — targets Gazebo Harmonic (not Fortress), requires NVIDIA OptiX/CUDA, incompatible with ROS 2 Humble stack. Cite when explaining why the Fortress gap remains open despite partial solutions. |

---

## 3a. Vibration-induced noise in LiDAR

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 49 | **B. Schlager et al.**, "Experimental Evaluation of Vibration Influence on a Resonant MEMS Scanning System for Automotive Lidars," *IEEE Open Journal of Intelligent Transportation Systems*, vol. 2, pp. 87–99, 2021. [Xplore](https://ieeexplore.ieee.org/document/9380978/) | Only paper testing a complete LiDAR system (Ouster OS1-64) on a shaker table (6–2000 Hz). Finds point dropout independent of vibration parameters. No parametric noise model derived. **Primary prior art for vibration characterization gap** — cite in RESEARCH_PLAN §3.2. Already in RESEARCH_PLAN §9 as [45]. |
| 50 | **R. Brazeal, B. Wilkinson, and R. Hochmair**, "A Rigorous Observation Model for the Risley Prism-Based Livox Mid-40 Lidar Sensor," *Sensors*, vol. 21, no. 14, 4722, 2021. [MDPI](https://www.mdpi.com/1424-8220/21/14/4722) | Simulates Risley prism misalignment under vibration; finds range largely unaffected, angular accuracy degrades. **Not validated experimentally** — the gap this study fills for Mid-360. Already in RESEARCH_PLAN §9 as [46]. |
| 51 | **Dong et al.**, "Vibration-aware Lidar-Inertial Odometry based on Point-wise Post-Undistortion Uncertainty," arXiv:2507.04311, 2025. [arXiv](https://arxiv.org/abs/2507.04311) | Models undistortion residual uncertainty under vibration in LIO but treats intrinsic LiDAR range noise as a fixed constant. Closest related work to vibration characterization — differentiates from this study in that we characterize intrinsic noise, not undistortion residuals. |
| 52 | **C. Periu et al.**, "Isolation of Vibrations Transmitted to a LIDAR Sensor Mounted on an Agricultural Vehicle," *Canadian Biosystems Engineering*, 2013. [Semantic Scholar](https://www.semanticscholar.org/paper/Isolation-of-Vibrations-Transmitted-to-a-LIDAR-on-Periu/b9af26b6901745993eab92c356ffd47ba0441975) | Agricultural LiDAR on tractor — positioning error increases 27% with speed. Old and different sensor/context but supports the general claim that platform motion affects LiDAR noise statistics. |

---

## 4. RealSense D455, RGB-D, thermal drift, FPN

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 17 | **Intel**, "Mitigation of Repetitive Pattern Effect of Intel RealSense Depth Cameras D400 Series," Whitepaper rev. 0.3. [PDF](https://www.realsenseai.com/wp-content/uploads/2025/06/Mitigate-Repetitive-Pattern-Effect-Whitepaper_v03.pdf) | Documents repetitive-pattern and projector artefacts on D400; supports Reality Gap discussion for Session D (visual/depth). |
| 18 | **Intel**, "Intel RealSense Self-Calibration for D400 Series Depth Cameras," Developer doc rev. 2.7. [Docs](https://dev.intelrealsense.com/docs/self-calibration-for-depth-cameras) | Self-calibration and thermal drift; cite when describing D455 intrinsic drift and need for periodic/thermal-aware calibration. |
| 19 | **D. P. Haefner & S. D. Burks**, "Measurements and metrics of fixed pattern noise: a new procedure for thermal camera noise measurement," SPIE 2023. [ADS](https://ui.adsabs.harvard.edu/abs/2023SPIE12533E..0TH/abstract) | Rigorous FPN and thermal noise methodology; transferable to your AprilTag-based camera characterisation and FPN discussion. |
| 20 | **Intel RealSense**, "Inter cam sync mode option not working," GitHub issue #10516 (librealsense). [GitHub](https://github.com/IntelRealSense/librealsense/issues/10516) | Real-world sync issues with D455; useful when writing about temporal sync (PTP/NTP) and multi-cam or multi-sensor timing. |
| 21 | **L. Chen et al.**, "A Temperature Drift Suppression Method of Mode-Matched MEMS Gyroscope Based on Mode Reversal and Multiple Regression," *Micromachines* 13, 1557, 2022. [MDPI](https://www.mdpi.com/2072-666X/13/10/1557) | MEMS gyro temperature drift modelling; supports your M4 thermal term and warm-up / τ_T discussion. |
| 22 | **M. Brenner et al.**, "RGB-D and Thermal Sensor Fusion: A Systematic Literature Review," arXiv:2305.11427, 2023. [arXiv](https://arxiv.org/pdf/2305.11427) | Survey of RGB-D and thermal fusion; useful if you extend to thermal or multi-modal analysis, or need a broad sensor-fusion citation. |

---

## 5. Sim-to-real, sensor model fidelity, domain adaptation

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 23 | **Q. Dai et al.**, "Domain Randomization-Enhanced Depth Simulation and Restoration for Perceiving and Grasping Specular and Transparent Objects," arXiv:2208.03792, 2022. [arXiv](https://arxiv.org/pdf/2208.03792v2) | DREDS: depth simulation with realistic sensor noise + restoration; strong support for "metrological simulation" and depth model fidelity. |
| 24 | **L. Campanaro et al.**, "Roll-Drop: accounting for observation noise with a single parameter," arXiv:2304.13150, 2023. [arXiv](https://arxiv.org/pdf/2304.13150v1) | Simple method to robustify policies to sensor noise in sim-to-real; useful when discussing robustness of SLAM to noise levels. |
| 25 | **Y. Kadokawa et al.**, "Cyclic Policy Distillation: Sample-Efficient Sim-to-Real Reinforcement Learning with Domain Randomization," arXiv:2207.14561, 2022. [arXiv](https://arxiv.org/pdf/2207.14561v2) | Domain randomization over physics and sensor; supports motivation that sensor model fidelity matters before policy learning. |
| 26 | **D. Nguyen et al.**, "TrueCity: Real and Simulated Urban Data for Cross-Domain 3D Scene Understanding," arXiv:2511.07007, 2025. [arXiv](https://arxiv.org/pdf/2511.07007v1) | Paired real + simulated urban data to quantify domain gap; analogous to your three-condition design (real / sim M1 / sim M4). |
| 27 | **I. Akinola et al.**, "TacSL: A Library for Visuotactile Sensor Simulation and Learning," arXiv:2408.06506, 2024. [arXiv](https://arxiv.org/pdf/2408.06506v2) | Sensor simulation library with sim-to-real focus; precedent for releasing a "metrological plugin" as software contribution. |
| 28 | **J. Song et al.**, "OceanSim: A GPU-Accelerated Underwater Robot Perception Simulation Framework," arXiv:2503.01074, 2025. [arXiv](https://arxiv.org/pdf/2503.01074v2) | Physics-based sensor simulation (underwater); supports trend toward high-fidelity sensor models in simulation. |
| 29 | **Y. Guo et al.**, "SPARR: Simulation-based Policies with Asymmetric Real-world Residuals for Assembly," arXiv:2602.23253, 2026. [arXiv](https://arxiv.org/pdf/2602.23253v1) | Residual policy for sim-to-real; mentions compensating for "sensor noise" in real world — good for Related Work on sim-to-real. |
| 30 | **T. Zhang et al.**, "HuB: Learning Extreme Humanoid Balance," arXiv:2505.07294, 2025. [arXiv](https://arxiv.org/pdf/2505.07294v2) | Identifies "sim-to-real gap caused by sensor noise and unmodeled dynamics"; useful as a recent citation that sensor fidelity matters. |
| 31 | **Y. Yan et al.**, "Efficiently Learning Robust Torque-based Locomotion Through Reinforcement with Model-Based Supervision," arXiv:2601.16109, 2026. [arXiv](https://arxiv.org/pdf/2601.16109v1) | Addresses "inaccurate dynamics modeling and sensor noise" with residual RL; supports your framing of sensor model as first-order gap. |
| 32 | **Q. Zeng et al.**, "CMR: Contractive Mapping Embeddings for Robust Humanoid Locomotion on Unstructured Terrains," arXiv:2602.03511, 2026. [arXiv](https://arxiv.org/pdf/2602.03511v1) | Bounds return gap under observation noise; theoretical angle on robustness to sensor noise, useful for Discussion. |
| 33 | **J. Yin et al.**, "Learning In-Hand Translation Using Tactile Skin With Shear and Normal Force Sensing," arXiv:2407.07885, 2024. [arXiv](https://arxiv.org/pdf/2407.07885v2) | "Sensor model for tactile skin that enables zero-shot sim-to-real transfer"; another example of sensor model enabling transfer. |
| 34 | **H. Bai et al.**, "Analyzing Material Recognition Performance of Thermal Tactile Sensing using a Large Materials Database and a Real Robot," arXiv:1711.01490, 2017. [arXiv](https://arxiv.org/pdf/1711.01490v3) | Analyses "sensor noise" and sim-to-real transfer for tactile sensing; supports general point that sensor models affect transfer. |
| 35 | **W. Xu et al.**, "Differentiable Fluid Physics Parameter Identification Via Stirring," arXiv:2311.05137, 2023. [arXiv](https://arxiv.org/pdf/2311.05137v1) | "Refining neural network to bridge sim-to-real gap and mitigate sensor noise-induced inaccuracies"; short citation for sensor noise in sim-to-real. |
| 36 | **K. Lv et al.**, "UniStateDLO: Unified Generative State Estimation and Tracking of Deformable Linear Objects Under Occlusion," arXiv:2512.17764, 2025. [arXiv](https://arxiv.org/pdf/2512.17764v1) | Mentions "sensor noises" and "zero-shot sim-to-real generalization"; useful if you discuss robustness to noise in perception. |

---

## 5a. Sim-to-real statistical validation and equivalence testing

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 56 | **S. Wellek**, *Testing Statistical Hypotheses of Equivalence and Noninferiority*, 2nd ed., Chapman & Hall/CRC, 2010. | The reference book for equivalence testing. Reviewers of Measurement and IEEE TIM will know it. Cite in METHODOLOGY §3.4 alongside Schuirmann and Lakens. Already in RESEARCH_PLAN §9 as [48]. |
| 57 | **M. Jongeneel et al.**, "Evaluating the Sim-to-Real Gap for Contact-Rich Robotic Manipulation," submitted to *IEEE RA-L*, 2024. [HAL](https://hal.science/hal-04673156) | Most rigorous quantitative sim-to-real comparison in contact-rich manipulation — and still uses RMSE, not equivalence testing. **Cite in RESEARCH_PLAN §3.4 as the example of the methodological gap TOST fills.** Already in RESEARCH_PLAN §9 as [43]. |
| 58 | **B. Acosta et al.**, "Validating Robotics Simulators on Real-World Impacts," *RA-L*, 2022. [arXiv](https://arxiv.org/abs/2110.00541) | Compares Drake, MuJoCo, PyBullet against real impact data — descriptive validation, no equivalence testing. Supports the argument that the community lacks rigorous sim-to-real validation methodology. |

---

## 6. Trajectory evaluation, ATE/RPE, alignment

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 37 | **S. Umeyama**, "Least-squares estimation of transformation parameters between two point patterns," *IEEE TPAMI* 13(4), 376–380, 1991. *(Already [15] in RESEARCH_PLAN.)* | Standard ref for Umeyama alignment used by evo; cite in METHODOLOGY when describing ATE/RPE computation. |

---

## 7. SLAM backends, LIO, visual–inertial

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 38 | **J. Liu and F. Zhang**, "Livox-Mapping: A LiODOM for Livox LiDARs," arXiv:2104.10831, 2021. *(Already [2] in RESEARCH_PLAN.)* | Core Livox degeneracy and mapping reference; use when discussing Mid-360 Rosetta and geometric degeneracy. |
| 39 | **R. Mur-Artal and J. D. Tardós**, "ORB-SLAM2," *IEEE TRO* 33(5), 2017. *(Already [8].)* | Standard ref for ORB-SLAM2/3 in your backend table; no extra pool entry needed. |

---

## 8. Datasets, benchmarks

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 40 | **W. Wang et al.**, "TartanAir: A Dataset to Push SLAM to New Limits," IROS 2020. *(Already [6].)* | Reality Gap and visual/SLAM; cite when comparing your design to existing sim–real benchmarks. |
| 41 | **A. Kadian et al.**, "Sim2Real Predictivity," *RA-L* 5(4), 2020. *(Already [5].)* | Formal Sim2Real predictivity; use in Related Work alongside Carlson and DREDS. |

---

## 9. Industrial / manufacturer and standards

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 42 | **ABB**, "IRB 14000 YuMi — Product specification." *(Already [16].)* | Official repeatability ±0.02 mm; keep as primary source for ground-truth specs. |
| 43 | **Intel**, "IMU Calibration Tool for Intel RealSense Depth Cameras (D435i, D455, L515)," Whitepaper 1.4, July 2020. *(Now [20] in RESEARCH_PLAN.)* | Official D455 IMU calibration; for static characterisation and calibration protocol. |

---

## 9a. Hand-eye, calibration, sync

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 44 | **easy_handeye** (ROS) and Tsai–Lenz / AX=XB: standard refs in EXPERIMENTAL_DESIGN §10; add a citation to a calibration paper (e.g. Tsai & Lenz, or a recent hand–eye survey) if a reviewer asks. | When you add it: choose one hand–eye survey or the original Tsai/Lenz for AX=XB. |
| 45 | **PTP IEEE 1588 / NTP**: document in EXPERIMENTAL_DESIGN §9; no single paper required unless you adopt a specific sync protocol from the literature. | If you cite: pick a short IEEE or timing-sync paper when you fix the protocol. |

---

## 10. Force/Torque sensors — future P2 direction

> These references are not cited in the current Phase I documents. They are collected here for when P2 (F/T sensor metrological validation) is formally designed. Do not include in Phase I manuscript.

| Ref | Citation | Why it may interest you |
|-----|----------|--------------------------|
| 59 | **Qiao et al.**, "SDI: A sparse drift identification approach for force/torque sensor calibration in industrial robots," *Neurocomputing*, 2025. [OpenReview](https://openreview.net/forum?id=Vg2aDO5BUe) | Sparse Bayesian learning for F/T drift via Kalman smoother. State of the art in F/T calibration — uses fixed covariance. No state-dependent model. Your P2 would be the first to fit state-dependent covariance for F/T. |
| 60 | **GRU temperature compensation**, "Temperature Compensation Method of Six-Axis Force/Torque Sensor Using Gated Recurrent Unit," *IEEE Sensors Journal*, 2025. [arXiv](https://arxiv.org/html/2502.17528v1) | GRU reduces temperature-induced F/T drift from 26 N to 2.7 N. Shows thermal drift is severe and learnable — but uses black-box model. Your P2 would do the same with explicit parametric model analogous to M4. |
| 61 | **Nitsche et al.**, "Dynamic characterization of multi-component sensors for force and moment," *JSSS*, 2018. [Copernicus](https://jsss.copernicus.org/articles/7/577/2018/) | PTB dynamic F/T characterization up to 2 kHz using electrodynamic shakers. Gold standard for dynamic F/T metrology — but requires expensive infrastructure unavailable in most robotics labs. Your P2 would use the YuMi as an accessible alternative protocol. |
| 62 | **ForceVLA**, "Enhancing VLA Models with a Force-aware MoE for Contact-rich Manipulation," arXiv:2505.22159, NeurIPS 2025. [arXiv](https://arxiv.org/abs/2505.22159) | Force-aware foundation model — 23.2% improvement with F/T as modality. **Primary demand signal for P2:** these models train on simulated F/T data and need accurate sensor models that don't exist yet. |
| 63 | **FD-VLA**, "Force-Distilled Vision-Language-Action Model for Contact-Rich Manipulation," arXiv:2602.02142, 2026. [arXiv](https://arxiv.org/html/2602.02142) | Distills force awareness into vision-only models. Same demand signal as ForceVLA — F/T sim-to-real gap directly limits model performance. Supports the strategic case for P2 timing. |

---

## How to use this pool

- **For the manuscript:** Pull refs from §1, §2, §3a, §5, §5a for Allan Variance, robot arm ground truth, vibration characterization, sim-to-real, and TOST methodology.
- **For experiments:** Use §2, §3, §4 when you hit issues (e.g. extrinsics, FPN, sync, thermal drift, cable routing, warm-up).
- **For reviewers:** Use §1, §2, §3a, §5a when they ask for support for AVAR, ground truth, vibration gap, or equivalence testing.
- **For P2 planning:** Use §10 when designing the F/T sensor metrological validation study.
- **Deduplication:** RESEARCH_PLAN §9 contains [1]–[16] and [17]–[21] (original) plus [40]–[48] (added 2026-03-23). When citing from this pool in the manuscript, use the RESEARCH_PLAN reference number if it exists; otherwise add to §9 with the next free number.

---

*Last updated: 2026-03-23 (post adversarial novelty audit — refs [46]–[63] added).*
