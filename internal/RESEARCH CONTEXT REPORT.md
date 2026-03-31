# RESEARCH CONTEXT REPORT
## Metrological Sensor Validation for Robotics Simulation — Key Literature & Conclusions

---

### 1. ANCHOR PAPER — Zhang 1999

**Referencia completa verificada:**
> Zhang, Z. (2000). *A Flexible New Technique for Camera Calibration.* IEEE Transactions on Pattern Analysis and Machine Intelligence, 22(11), 1330–1334. DOI: 10.1109/34.888718

**Relevancia para este estudio:**
No inventó la calibración de cámaras — ese problema ya existía con equipamiento caro (planos ortogonales, cubos de precisión). Lo que hizo fue dar al campo un protocolo tan riguroso y accesible (un tablero de ajedrez impreso) que se convirtió en estándar universal. Integrado en OpenCV. Premio IEEE Helmholtz Test of Time 2013. El espíritu de este estudio es análogo: no crear algo nuevo, sino cerrar un loop que nadie ha cerrado formalmente.

**Cita directa del propio Zhang en retrospectiva (Machine Vision and Applications, 2016):**
> *"I developed the technology initially for my own need, and I did not have any idea that my work would have this sort of lasting impact."*

---

### 2. SIM-TO-REAL GAP — EVIDENCIA CUANTITATIVA

**Paper de referencia principal verificado:**
> Aljalbout et al. (2025). *The Reality Gap in Robotics: Challenges, Solutions, and Best Practices.* Annual Review of Robotics. arXiv: 2510.20808

Confirma estructuralmente los siguientes datos cuantitativos citados en conversación y verificados en Iris Publishers / literatura de revisión:

- **70% de discrepancia** en fricción articular estática entre simulación y realidad — causa fallos catastróficos en despliegue de políticas RL
- **83% de discrepancia** en tareas de manipulación de telas (análisis 2024) por ignorar amortiguación por cizallamiento en simuladores de cuerpo rígido
- Contacto físico, fricción no-lineal, y backlash mecánico raramente modelados — siendo exactamente los fenómenos más críticos para manipulación

**Mecanismo del fallo estructural (verificado):**
Los simuladores usan contactos puntuales, conos de fricción linealizados y sistemas spring-damper para mantener eficiencia computacional. Estas aproximaciones producen artefactos no físicos: fuerzas internas espurias, agarres inestables, patrones de movimiento irreales.

---

### 3. TRANSIC — CUANTIFICACIÓN DEL GAP EN MANIPULACIÓN

**Referencia completa verificada:**
> Jiang, Y., Wang, C., Zhang, R., Wu, J., & Fei-Fei, L. (2024). *TRANSIC: Sim-to-Real Policy Transfer by Learning from Online Correction.* Conference on Robot Learning (CoRL) 2024. arXiv: 2405.10315

**Dato clave verificado:**
El mejor método baseline (IWR) alcanza solo un **18% de tasa de éxito media** en presencia de gaps sim-to-real deliberadamente exacerbados. TRANSIC lo resuelve con intervención humana en el loop — lo que implica que la simulación sola, sin corrección humana online, es insuficiente para manipulación rica en contacto.

**Nota de uso:** TRANSIC aborda el gap desde el lado de la política (corrección humana). Tu estudio lo aborda desde el lado opuesto: la fidelidad del modelo de sensor. Son complementarios, no competidores.

---

### 4. GAZEBO NOISE MODELS — ESTADO DOCUMENTADO

**Fuente: Documentación oficial de Gazebo (Ignition / Classic)**

Gazebo soporta modelos de ruido gaussiano configurables via tag `<noise>` en SDF, con parámetros `mean`, `stddev`, `bias_mean`, `bias_stddev`. La propia documentación oficial reconoce explícitamente que:
- Los sensores sin configuración observan el mundo de forma perfecta (no hay ruido por defecto)
- El ruido gaussiano "puede no ser muy realista" pero es "mejor que nada" y una "buena aproximación de primer orden"
- Los valores de los tutoriales oficiales son elegidos para que "los efectos sean visibles" — no derivados de hardware real

**Conclusión documentada:** Los parámetros son placeholders por diseño. No existe en la documentación ningún procedimiento para derivarlos de caracterización de hardware real.

---

### 5. TOST — AUSENCIA EN ROBÓTICA (CLAIM CENTRAL)

**Estado verificado por búsqueda sistemática:**
La búsqueda de "TOST equivalence testing robotics simulation sensor validation SLAM" y variantes no devuelve ningún paper de robótica aplicando TOST a validación de modelos de sensor. Los únicos resultados son aplicaciones en farmacología (FDA/EMA bioequivalencia), biomasa forestal, y ensayos clínicos.

**Formulación precisa y defendible del claim:**
> *Ningún paper existente ha aplicado TOST con márgenes δ pre-especificados a priori para declarar equivalencia estadística entre modelos de sensor simulados y sensores reales en el contexto de validación de transferencia SLAM.*

**Por qué el t-test estándar es insuficiente (verificado en estadística):**
Un t-test con p > 0.05 no demuestra equivalencia — solo demuestra ausencia de evidencia para rechazar la hipótesis nula. Con muestras pequeñas, esto ocurre aunque los sistemas sean muy distintos. La robótica lleva años interpretando p > 0.05 como "suficientemente bueno", lo cual es estadísticamente incorrecto.

**Estándar de referencia:** FDA/EMA exigen TOST con IC 90% dentro de márgenes pre-especificados para declarar bioequivalencia. Lleva >40 años siendo el gold standard en farmacología. No existe equivalente en robótica.

---

### 6. METROLOGÍA DE SENSORES — LO QUE EXISTE Y LO QUE FALTA

**Lo que SÍ existe (fragmentado):**
- Allan Variance para IMUs — IEEE 952, estándar en navegación inercial
- Calibración de cámaras — Zhang 1999, universal
- Calibración extrínseca LiDAR-cámara con dianas certificadas
- ISO 9283 — caracterización de precisión y repetibilidad de robots industriales
- Benchmarks con ground truth metrológico (RTK-GPS, INS de referencia)

**Lo que NO existe (el gap):**
No hay pipeline estandarizado que:
1. Tome la caracterización metrológica real del sensor
2. La inyecte en el simulador como modelo de ruido parametrizado
3. Valide la equivalencia mediante test estadístico formal con márgenes predefinidos
4. Produzca un resultado interpretable antes del despliegue físico

Cada equipo construye ese puente de forma artesanal, o no lo construye.

---

### 7. PRECEDENTE HISTÓRICO RELEVANTE — ANALOGÍA ESTRUCTURAL

| Zhang 1999 | Este estudio |
|---|---|
| Calibración de cámaras: problema conocido, soluciones ad hoc incompatibles | Validación de sensor simulado: problema conocido, sin pipeline estándar |
| Equipamiento caro requerido (planos ortogonales de precisión) | Ground truth metrológico inasequible sin protocolo (YuMi como referencia) |
| Propuso protocolo riguroso y accesible con tablero de ajedrez | Propone pipeline M1→M4 con TOST como declaración formal |
| Publicó software junto al paper | Plugin Gazebo open-source antes del paper |
| Resultó en estándar de facto universal | Objetivo: protocolo reproducible adoptable como baseline |

---

### 8. ADVERTENCIAS PARA EL MODELO RECEPTOR

Los siguientes datos fueron citados en conversación **sin búsqueda directa verificada** en esta sesión — usar con precaución y verificar antes de citar:

- Furrer et al. 2016 — Allan Variance IMUs (existencia probable, referencia exacta no verificada)
- Liu & Zhang 2021 — caracterización LiDAR (no verificada)
- Lin 2022 — validación con laser tracker (no verificada)
- Wu et al. 2025 — TOST en ADAS (mencionado como única aproximación al claim, no verificado)
- Koos et al. — sim-to-real gap teórico (no verificada)

---

*Report generado a partir de conversación de investigación con búsquedas en tiempo real. Fecha: marzo 2026.*