# Documento de Auditoría Consolidada — slam-sensor-metrological-validation

**Repositorio:** [Narcis-Abella/slam-sensor-metrological-validation](https://github.com/Narcis-Abella/slam-sensor-metrological-validation)  
**Fecha de auditoría:** 2026-03-07  
**Fase del proyecto:** v0.3 — Diseño (sin datos experimentales recogidos)  
**Fuentes:** Dos auditorías académicas independientes (Audit 1 y Audit 2)

---

## Propósito de este documento

Este documento consolida todos los puntos auditados en las dos revisiones académicas del proyecto. Sirve como:

1. Checklist de revisión futura — antes de recoger datos, enviar al supervisor o someter a revista.
2. Registro de debilidades identificadas — con referencias a archivos y secciones concretas.
3. Guía de acciones correctivas — priorizadas por criticidad y esfuerzo.

Revisar en cada hito (pre-supervisor, pre-sesiones dinámicas, pre-manuscrito) y marcar los ítems resueltos.

---

## Tabla de contenidos

1. [Resumen de puntuaciones](#1-resumen-de-puntuaciones)
2. [Dimensión 1 — Novedad científica](#2-dimensión-1--novedad-científica)
3. [Dimensión 2 — Hipótesis y falsabilidad](#3-dimensión-2--hipótesis-y-falsabilidad)
4. [Dimensión 3 — Rigor del diseño experimental](#4-dimensión-3--rigor-del-diseño-experimental)
5. [Dimensión 4 — Modelado de ruido sensorial (M1–M4)](#5-dimensión-4--modelado-de-ruido-sensorial-m1m4)
6. [Dimensión 5 — Metodología estadística](#6-dimensión-5--metodología-estadística)
7. [Dimensión 6 — Selección y uso de backends SLAM](#7-dimensión-6--selección-y-uso-de-backends-slam)
8. [Dimensión 7 — Reproducibilidad y ciencia abierta](#8-dimensión-7--reproducibilidad-y-ciencia-abierta)
9. [Dimensión 8 — Calidad y completitud de referencias](#9-dimensión-8--calidad-y-completitud-de-referencias)
10. [Dimensión 9 — Viabilidad y alcance](#10-dimensión-9--viabilidad-y-alcance)
11. [Top 5 problemas críticos consolidados](#11-top-5-problemas-críticos-consolidados)
12. [Expansiones (A, B, A+B)](#12-expansiones-a-b-ab)
13. [Veredicto de publicación por revista](#13-veredicto-de-publicación-por-revista)
14. [Checklist de revisión pre-hito](#14-checklist-de-revisión-pre-hito)

---

## 1. Resumen de puntuaciones

| # | Dimensión | Audit 1 | Audit 2 | Consenso |
|---|-----------|---------|---------|----------|
| 1 | Novedad científica | 6/10 | 7/10 | Media 6.5 |
| 2 | Hipótesis y falsabilidad | 7/10 | 8/10 | Media 7.5 |
| 3 | Rigor diseño experimental | 7/10 | 8/10 | Media 7.5 |
| 4 | Modelo de ruido M1–M4 | 5/10 | 7/10 | Media 6 |
| 5 | Metodología estadística | 4/10 | 6/10 | Crítico |
| 6 | Backends SLAM | 7/10 | 8/10 | Media 7.5 |
| 7 | Reproducibilidad | 6/10 | 6/10 | Media 6 |
| 8 | Referencias | 3/10 | 8/10 | Discrepancia |
| 9 | Viabilidad y alcance | 6/10 | 7/10 | Media 6.5 |

---

## 2. Dimensión 1 — Novedad científica

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §3.6, §3.7
- `README.md` §0, §5.1

### Afirmación de novedad actual

> "No study has combined (1) kinematic-state-dependent noise models derived from dynamic ground truth, (2) validation across multiple tight-coupled SLAM backends, and (3) statistical comparison against a sub-millimetre industrial manipulator reference."

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Afirmación estructurada; M4 es el objeto teórico más claro; YuMi como referencia cinemática es diferenciador. | Competidores cercanos no identificados; papers críticos de SLAM/sensor no citados; M4 presentado como fórmula única para IMU/LiDAR/cámara cuando los mecanismos físicos son distintos. |
| Audit 2 | Gap explícito; framing distinto vs Sim2Real clásico; M4 es objeto concreto. | M4 percibido como heurístico; afirmación "no prior work" frágil en RA-L/T-RO; novedad del dataset no desarrollada como clase de contribución. |

### Referencias faltantes o débiles

- EuRoC MAV dataset (Burri et al., 2016) — benchmark visual-inertial de referencia.
- TUM-VI benchmark (Schubert et al., 2018) — caracterización explícita de ruido IMU con Allan Variance (BMI160), comparable a BMI055.
- Hilti SLAM Challenge — ground truth de alta calidad.
- Rehder et al. (2016) "Extending kalibr" — calibración IMU-cámara continua con ground truth de brazo robótico.
- Furgale et al. (2013) "Unified temporal and spatial calibration" — base del toolchain kalibr.

### Acciones recomendadas

- [x] Añadir citas a EuRoC, TUM-VI, Hilti SLAM Challenge; indicar qué ground truth usan (motion capture / laser tracker) vs. YuMi.
- [x] Citar y distinguir de Rehder et al. (2016) y Furgale et al. (2013) en kalibr.
- [ ] Añadir tabla de novedad (2×4: trabajo previo vs. este trabajo en cuatro dimensiones: tipo de sensor, fuente de ground truth, modelo de ruido dinámico, evaluación multi-backend).
- [ ] Reforzar el argumento físico por sensor para M4 en `RESEARCH_PLAN.md` §3.6.
- [ ] Posicionar explícitamente el dataset como contribución en `RESEARCH_PLAN.md` §6.2–6.3 y `README.md`.

---

## 3. Dimensión 2 — Hipótesis y falsabilidad

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §4
- `docs/METHODOLOGY.md` §3.4

### Hipótesis actuales

- H0: Simulación metrológica vs. hardware real → ATE estadísticamente indistinguible (p > 0.05).
- H1: Calidad del IMU afecta sistemáticamente al rendimiento SLAM.
- H2: Asimetría CW/CCW observable en bias del giroscopio.

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | H0/H1/H2 claros; criterio de éxito pre-registrado; H0 rechazada también publicable. | Error lógico crítico: p > 0.05 ≠ equivalencia; "ausencia de evidencia no es evidencia de ausencia"; se requiere test de equivalencia (TOST). |
| Audit 2 | H0/H1/H2 operacionales; criterios de éxito definidos; enlace hipótesis–pipeline claro. | Sin margen de equivalencia pre-declarado; múltiples análisis secundarios no priorizados. |

### Problema estadístico central

El diseño actual usa:

- Test: H0: μ_M = μ_R vs. H1: μ_M ≠ μ_R
- Criterio de éxito: p > 0.05 (no rechazar H0)

Problema: un p > 0.05 con n = 9 indica potencia insuficiente para detectar diferencias, no evidencia positiva de equivalencia. En revistas metrológicas (IEEE TIM, Measurement) esto se considera un error lógico.

Solución: TOST (Two One-Sided Tests) de bioequivalencia:

1. Pre-especificar margen δ (ej. δ = 5 mm ATE, o δ = 10% del ATE de referencia de T1).
2. Probar H_lower: μ_M − μ_R > −δ y H_upper: μ_M − μ_R < δ simultáneamente.
3. Aceptar equivalencia si ambas se aceptan.
4. Citar Schuirmann (1987) o Lakens (2017) "Equivalence Testing for Psychological Research".

### Acciones recomendadas

- [x] Sustituir el criterio de éxito de H0 por TOST con margen δ predefinido.
- [x] Definir δ en unidades de ATE (ej. δ = 10% del peor ATE real de T3).
- [x] Realizar análisis de potencia formal para justificar n = 9 o aumentar n (típicamente n ≥ 20–30 para TOST con 80% potencia).
- [x] Definir endpoints primarios vs. exploratorios; H1 y H2 pueden mantener tests direccionales estándar.
- [x] Declarar explícitamente que resultados negativos son aceptables y se reportarán.

---

## 4. Dimensión 3 — Rigor del diseño experimental

### Ubicación en el repositorio

- `docs/EXPERIMENTAL_DESIGN.md`
- `docs/HARDWARE_PAYLOAD.md` §1–2
- `docs/METHODOLOGY.md` §2.4

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Estructura en dos etapas correcta; diseño T1/T2/T3 con bloques CW/CCW/MIX bien justificado; 60 s estáticos; tabla de variables de confusión. | YuMi repeatability vs. volumetric accuracy no resuelto para ATE; trayectorias cortas (150–300 mm) vs. 10–100 m típicos; ground truth: ¿comandado vs. ejecutado? (blending en esquinas). |
| Audit 2 | Diseño de ground truth bien pensado; sync y hand-eye no son afterthoughts; variables de confusión controladas; diseño de trayectorias rico. | Objetivos numéricos de sync no fijados; sin protocolo para rechazar sesiones por deriva ambiental; tiempo de robot alto (~32 h). |

### Repeatability vs. accuracy del YuMi

- Repeatability ±0.02 mm: Consistencia al volver a la misma pose desde la misma dirección.
- Volumetric / path-following accuracy: Error sistemático entre pose comandada y pose real en un frame absoluto. Incluye errores de encoders, flexión estructural bajo carga, blending geométrico en esquinas.
- Estimación: Path-following accuracy típicamente 0.1–0.5 mm (5–25× mayor que repeatability).
- Implicación: ATE es métrica absoluta; si el ground truth tiene ±0.5 mm de incertidumbre sistemática, afirmaciones de diferencias de pocos mm pueden ser inválidas.

### Sincronización temporal

- Cálculo: 10 ms a 100 mm/s ≈ 1 mm de error espacial.
- Gap: no se declara un objetivo numérico (ej. |Δt| ≤ 3 ms con PTP, ≤ 5 ms con NTP).
- PTP vs. NTP: Capacidad del IRC5 como PTP grandmaster/slave debe confirmarse con documentación ABB.

### Acciones recomendadas

- [x] Cuantificar path-following accuracy del YuMi (documentación ABB o medición empírica); incluir en presupuesto de incertidumbre §2.4.
- [ ] Aclarar si el ground truth usa trayectoria comandada o ejecutada (encoder state); si es comandada, documentar el efecto del blending en T3.
- [ ] Fijar objetivos numéricos de sync: ej. "|Δt| ≤ 3 ms (PTP) o ≤ 5 ms (NTP) antes de aceptar sesión".
- [ ] Añadir checklist de "criterios de aceptación de sesión" en `EXPERIMENTAL_DESIGN.md` (ATE floor, deriva de temperatura, sync, residual hand-eye).
- [ ] Definir protocolo para rechazar/anotar sesiones si temperatura o iluminación exceden umbral.
- [ ] Planificar qué sesiones son imprescindibles vs. "nice to have" si el tiempo de laboratorio es limitado.

---

## 5. Dimensión 4 — Modelado de ruido sensorial (M1–M4)

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §3.6
- `docs/METHODOLOGY.md` §4–5
- `README.md` §5.1

### Fórmula M4 actual

$$
\sigma^2(t) = \sigma^2_{\mathrm{static}}(t_{\mathrm{on}}(t)) + c_v \|\omega\| + c_a \|a\| + c_j \|\dot{a}\|
$$

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Motivación física buena; estrategia de cross-validation (fit T1+T2, eval T3) correcta. | Inconsistencia dimensional: sumar σ² (unidades²) con ||ω|| (unidades) requiere definición explícita de c_v, c_a, c_j por sensor; riesgo de σ² < 0 si coeficientes negativos; anisotropía ignorada (MEMS es axis-dependent); identificabilidad de 6 parámetros con O(9) muestras no abordada. |
| Audit 2 | M1–M3 sólidos; M4 anclado en literatura; generalización T3 pre-planeada. | Identificabilidad y acoplamiento de coeficientes no abordados; modelo de cámara hand-wavy; LiDAR sin tratamiento explícito de bias. |

### Problemas técnicos específicos

1. Dimensionalidad: Para IMU giroscopio [unidades (rad/s)²], c_v necesitaría [(rad/s)²/(rad/s)] = [rad/s]. Debe declararse por sensor y eje.
2. No-negatividad: Forma lineal permite σ² < 0 si los datos requieren coeficientes negativos. Alternativa multiplicativa: σ²(t) = σ²_static × (1 + c_v||ω|| + c_a||a|| + c_j||ȧ||) garantiza positividad.
3. Colinealidad: En T2, ||ω||, ||a||, ||ȧ|| están correlacionados; c_v, c_a, c_j pueden ser individualmente no identificables.
4. Anisotropía: Ruido MEMS es axis-dependent (g-sensitivity, coeficiente térmico); un único σ² para todos los ejes es simplificación que puede enmascarar efectos relevantes para H2.

### Acciones recomendadas

- [x] Reescribir fórmula como multiplicativa o añadir restricción de no-negatividad en el ajuste.
- [x] Definir unidades de c_v, c_a, c_j explícitamente por tipo de sensor y eje.
- [x] Añadir subsección de identificabilidad en `METHODOLOGY.md` §5: VIF, número de condición de la matriz de diseño.
- [x] Considerar regularización (ridge L2) si el ajuste está mal condicionado.
- [x] Declarar limitación de anisotropía; para H2 considerar análisis por eje.
- [x] Separar conceptualmente variance vs. bias en LiDAR; en cámara, distinguir drift térmico (sistemático) vs. motion blur (aleatorio).
- [x] Permitir sensor-specific pruning: ej. "Para LiDAR solo c_v; c_j no identificable, fijado a 0."

---

## 6. Dimensión 5 — Metodología estadística

### Ubicación en el repositorio

- `docs/METHODOLOGY.md` §3

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Pipeline Shapiro-Wilk → paramétrico/no-paramétrico; efecto (Cohen's d, rank-biserial); Bonferroni presente. | Error fundamental: criterio H0 (p > 0.05) no proporciona evidencia de equivalencia; Bonferroni cubre 12 comparaciones pero la matriz completa puede tener ~216; n = 9 da ~35% potencia para d = 0.5; TOST requiere n ≥ 20–30. |
| Audit 2 | Test selection y effect sizes correctos; Bonferroni sobre 12 comparaciones apropiado; incertidumbre ground truth ligada a interpretación. | Tamaño muestral y potencia no abordados; sin plan para estructura jerárquica (repeticiones dentro de bloque dentro de sesión); ATE/RPE tratados como escalares pero backends y trayectorias multiplican comparaciones. |

### Matriz de comparaciones

- Diseño actual: 4 sesiones × 3 trayectorias = 12 comparaciones primarias.
- Matriz completa: 4 × 3 × (2–3 backends) × 3 CFG × 2 métricas (ATE/RPE) ≈ 216 comparaciones.
- Bonferroni con α/12 es optimista por factor ~18 para la matriz completa.
- Recomendación: Pre-especificar comparaciones primarias (con Bonferroni) y marcar el resto como exploratorias (reportar sin corrección pero señaladas).

### Acciones recomendadas

- [x] Implementar TOST para H0 (ver Dimensión 2).
- [x] Realizar y documentar análisis de potencia en `METHODOLOGY.md` §3.
- [x] Aumentar n (5–10 repeticiones por bloque) o reducir comparaciones primarias si la potencia es insuficiente.
- [x] Definir conjunto de endpoints primarios (ej. ATE RMSE bajo FAST-LIO2 Session D T2, ORB-SLAM3 Session B T2); resto exploratorio.
- [ ] Considerar modelo de efectos mixtos para el manuscrito final (random effects por trayectoria/bloque).
- [x] Usar Holm-Bonferroni o Benjamini-Hochberg si se reporta la matriz completa.

---

## 7. Dimensión 6 — Selección y uso de backends SLAM

### Ubicación en el repositorio

- `docs/SLAM_BACKENDS.md`

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Cobertura paradigmática excelente; configuración congelada correcta; exclusión de LIO-SAM justificada. | Session A "IMU preintegration" no es backend SLAM (es dead reckoning abierto); GLIM requiere GPU (reproducibilidad); Session C (2D LiDAR) menos interesante científicamente. |
| Audit 2 | Cobertura ejemplar; estrategia "frozen configuration" sólida; LIO-SAM excluido con justificación. | Riesgo de sobre-complejidad; backends visual pueden tener problemas de madurez ROS2; sin validación previa en EuRoC/TUM-VI. |

### Puntos específicos

1. Session A — IMU preintegration: Es integración abierta sin observaciones; drift O(t³). Debe enmarcarse como "benchmark de drift IMU abierto" no como "backend SLAM".
2. GLIM: Solo GPU (CUDA); labs sin NVIDIA no pueden replicar. Declarar como limitación; considerar alternativa CPU (ej. HDL-Graph-SLAM).
3. Session C (2D LiDAR): Tecnología madura; incertidumbre H0 baja. Candidata a reducir a resultado baseline breve si hay que recortar scope.
4. Validación previa: Planificar ejecución de cada backend en EuRoC/TUM-VI/Newer College antes de usarlo como "instrumento de medida".

### Acciones recomendadas

- [ ] Reformular Session A como "open-loop IMU preintegration drift benchmark".
- [ ] Declarar limitación de GPU para GLIM.
- [ ] Definir subconjunto "core" de backends por modalidad (ej. FAST-LIO2 + GLIM para Mid-360); marcar otros como "bonus si hay tiempo".
- [ ] Añadir paso de sanity-check: validar cada backend en un dataset público estándar antes del uso metrológico.
- [ ] Pre-definir criterios de fallo (ej. exclusión, máximo N re-ejecuciones).

---

## 8. Dimensión 7 — Reproducibilidad y ciencia abierta

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §6.4
- `README.md` §7, §10

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Intenciones explícitas: dataset público, plugin Gazebo, scripts Allan, pipeline evo; PROGRESS_LOG ejemplar. | "Planned for release" insuficiente sin: (a) DOI, (b) formato de datos, (c) metadata; plugin Rosetta no iniciado — es deliverable crítico. |
| Audit 2 | Intenciones open-source claras; documentación organizada; detalle metodológico alto. | Dataset no planificado concretamente; scripts de análisis no scoped; sin licencia de datos. |

### Gaps de especificación

- DOI: Zenodo o IEEE DataPort estándar para datasets de robótica.
- Formato: ROS2 bags MCAP vs. ASCII KITTI/TUM; cuál se publicará.
- Metadata: Archivos de calibración (formato kalibr), offsets de sincronización medidos, geometría del entorno, logs de temperatura.
- Plugin Gazebo Rosetta: Implementar integración temporal del patrón Rosetta en Gazebo; tarea no trivial. Sin esto, la validación metrológica para LiDAR no es posible.
- Licencia de datos: Ej. CC-BY 4.0; no declarada.

### Acciones recomendadas

- [ ] Añadir sección "Reproducibilidad y liberación de datos" en `README.md` y `RESEARCH_PLAN.md`.
- [ ] Especificar: (i) D_static y D_dynamic_yumi se liberarán, (ii) hosting (Zenodo/IEEE DataPort), (iii) timeline (ej. upon acceptance).
- [ ] Definir estructura `analysis/` con scripts versionados y dependencias fijadas (requirements.txt / Conda env).
- [ ] Elegir y documentar licencia de datos (ej. CC-BY 4.0).
- [ ] Tratar el plugin Gazebo Rosetta como deliverable crítico en ruta; no como tarea de fondo.

---

## 9. Dimensión 8 — Calidad y completitud de referencias

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §9
- `docs/REFERENCES_POOL.md`

### Hallazgos de la auditoría

Discrepancia importante: Audit 1 puntúa 3/10 (backends no citados → riesgo desk reject); Audit 2 puntúa 8/10 (cobertura rica para TIM/Measurement).

### Citas obligatorias faltantes (Audit 1)

| Backend usado | Cita faltante |
|---------------|---------------|
| FAST-LIO2 | Xu et al. (2022), "Fast-LIO2: Fast Direct LiDAR-Inertial Odometry", IEEE RA-L |
| GLIM | Koide et al. (2023), "Globally Consistent 3D LiDAR Mapping with GPU-Accelerated GICP Matching Cost Factors" |
| ORB-SLAM3 | Campos et al. (2021), "ORB-SLAM3: An Accurate Open-Source Library...", IEEE TRO (solo ORB-SLAM2 citado) |
| Cartographer | Hess et al. (2016), "Real-Time Loop Closure in 2D LiDAR SLAM", ICRA |
| KISS-ICP | Vizzo et al. (2023), "KISS-ICP: In Defense of Point-to-Point ICP", IEEE RA-L |
| Point-LIO | He et al. (2023), "Point-LIO: Robust High-Bandwidth...", IEEE RA-L |
| OpenVINS | Geneva et al. (2020), "OpenVINS: A Research Platform for Visual-Inertial Estimation", ICRA |
| evo | Grupp (2017), "evo: A Python Package for the Evaluation of Odometry and SLAM" |

### Benchmarks faltantes

- EuRoC MAV (Burri et al., 2016)
- TUM-VI (Schubert et al., 2018)
- Newer College Dataset (Ramezani et al., 2020)

### Posible error de atribución

- Six-Position Test: Referido como "IEEE Std 952" en algún lugar; el estándar correcto para la metodología es IEEE Std 1293 (1998, reaffirmed). Verificar y corregir.

### Acciones recomendadas

- [x] Añadir las 8 citas de backends a `RESEARCH_PLAN.md` §9 y al manuscrito.
- [x] Añadir 3–4 referencias de benchmarks (Hilti, Newer College, EuRoC, TUM-VI).
- [x] Verificar y corregir estándar Six-Position Test (1293 vs. 952).
- [x] Citar Furgale et al. (2013) para kalibr.

---

## 10. Dimensión 9 — Viabilidad y alcance

### Ubicación en el repositorio

- `docs/RESEARCH_PLAN.md` §2, §6
- `docs/HARDWARE_PAYLOAD.md` §6
- `PROGRESS_LOG.md`

### Hallazgos de la auditoría

| Auditoría | Fortalezas | Debilidades |
|-----------|------------|-------------|
| Audit 1 | Scope Phase I correcto; MPU definido (static + Session D + M4 parcial); blockers priorizados. | Payload Session D en 70% (Mid-360 ~350 g + cables); PTP/NTP no resuelto; timeline agresivo; plugin no iniciado. |
| Audit 2 | Blockers explícitos; timeline realista si todo va bien; scope disciplinado. | Riesgo de ejecución alto; MPU no definido nítidamente; fallback YuMi (Mitsubishi) poco desarrollado. |

### Bloqueadores críticos

1. Payload Session D: Mid-360 ~350 g + cables USB/Ethernet ~30–50 g → 380–400 g. A 80% de 500 g, rendimiento dinámico YuMi se reduce; vibración en T3 puede violar criterio de settling.
2. Sincronización PTP/NTP: Capacidad del IRC5 como PTP grandmaster/slave debe confirmarse. NTP típicamente 1–10 ms jitter → hasta 1 mm espacial a velocidades T2.
3. Plugin Gazebo: No iniciado; en ruta crítica.

### Acciones recomendadas

- [ ] Verificar peso real con báscula antes de reservar YuMi.
- [ ] Definir "Phase I-core" explícito en `RESEARCH_PLAN.md` §6: ej. IMU + Mid-360, FAST-LIO2 + GLIM, M1–M4; resto extensiones opcionales.
- [ ] Expandir fallback Mitsubishi en `HARDWARE_PAYLOAD.md` §6: qué cambia (payload, repeatability, presupuesto).
- [ ] Añadir ítems de riesgo en `PROGRESS_LOG.md` (reserva YuMi, retrasos administrativos) con mitigaciones.
- [ ] Considerar timeline más conservador (manuscrito Q1–Q2 2027 si hay retrasos).

---

## 11. Top 5 problemas críticos consolidados

| # | Problema | Por qué causa rechazo | Acción específica |
|---|----------|------------------------|-------------------|
| 1 | Error de equivalencia estadística | p > 0.05 no demuestra equivalencia; revisores metrológicos rechazarán. | Implementar TOST con margen δ predefinido; actualizar `METHODOLOGY.md` §3.4; recalcular n. |
| 2 | Backends SLAM sin citar | Desk reject o major revision en Q1. | Añadir Xu, Koide, Campos, Hess, Vizzo, He, Geneva, Grupp a `RESEARCH_PLAN.md` §9. |
| 3 | YuMi repeatability ≠ accuracy para ATE | Revisor metrológico distinguirá; claims de significancia invalidadas si ground truth ±0.5 mm. | Cuantificar path-following accuracy; incluir en presupuesto §2.4; o medir con laser tracker/Vicon. |
| 4 | Identificabilidad y consistencia M4 | Revisor de modelado sensorial planteará los tres puntos (dimensional, no-negatividad, colinealidad). | Reescribir fórmula multiplicativa o añadir restricciones; VIF; regularización; en `METHODOLOGY.md` §5.3. |
| 5 | Tamaño muestral insuficiente | n = 9 da ~35% potencia; TOST requiere n ≥ 20–30. | Análisis de potencia formal; aumentar repeticiones o reducir comparaciones primarias. |

---

## 12. Expansiones (A, B, A+B)

### Expansion A — LiDAR repetitivo (spinning)

- Nuevas preguntas: Comportamiento de M4 para LiDAR spinning vs. solid-state; sensibilidad por backend (LIO-SAM); degeneración comparativa.
- Backends adicionales: LIO-SAM, LIO-SAM2, LeGO-LOAM.
- **Esfuerzo:** Sesión estática + dinámica (~8 h YuMi); plugin Gazebo para spinning; análisis M4 extendido.
- Bloqueador: Payload — spinning 16-beam típicamente 800–900 g; YuMi 500 g. Probablemente requiere Mitsubishi u otro robot.

### Expansion B — Visual-LiDAR-Inertial multimodal

- **Valor:** Consistencia cross-modal de M4; robustez de fusión a gaps por sensor.
- Necesidad: Sesión dedicada multi-sensor (Mid-360 + D455 co-montados); no basta reutilizar B y D por separado.
- Bloqueadores: Payload combinado ~625 g + mount excede 500 g YuMi; sincronización de tres relojes; complejidad de análisis.

### Expansion A+B combinada

- **Escala:** Realísticamente nivel PhD o multi-año.
- Para bachelor/master: No realista como deliverable único.
- Enfoque pragmático: Phase I → TIM/Measurement; Expansiones A/B como Phase II/III (tesis master o PhD).

---

## 13. Veredicto de publicación por revista

| Revista | Puntuación | Veredicto |
|--------|-----------|-----------|
| IEEE TIM | 6→8/10 con correcciones | Objetivo primario realista. Requiere TOST, power analysis, plan de datos. |
| Measurement | 7/10 | Muy buen encaje. Algo más flexible en SLAM. |
| RA-L | 4/10 | Stretch. Requiere expansión o insights más centrados en robótica. |
| T-RO | 3/10 | Muy ambicioso. Requiere contribución teórica profunda o benchmark excepcional. |

---

## 14. Checklist de revisión pre-hito

### Pre-revisión supervisor (v1.0)

- [x] TOST y margen δ definidos en METHODOLOGY
- [x] Citas de backends añadidas a RESEARCH_PLAN §9
- [ ] Phase I-core definido en RESEARCH_PLAN §6
- [x] Path-following accuracy YuMi documentada o en presupuesto
- [x] Estándar IEEE 1293 vs. 952 verificado

### Pre-sesiones dinámicas

- [ ] Peso verificado con báscula
- [ ] Método de sincronización (PTP/NTP) definido y documentado
- [ ] Criterios de aceptación de sesión en EXPERIMENTAL_DESIGN
- [x] Análisis de potencia documentado
- [ ] Montajes diseñados y validados

### Pre-manuscrito

- [ ] Plan de datos (DOI, formato, licencia) en README y RESEARCH_PLAN
- [x] Identificabilidad M4 documentada en METHODOLOGY
- [ ] Plugin Gazebo Rosetta funcional o estado documentado
- [x] Endpoints primarios vs. exploratorios claramente declarados
- [x] Referencias de benchmarks añadidas

---

*Documento generado el 2026-03-07. Revisar y actualizar al resolver ítems.*
