© 2025 Marcos Verrell Moss Ross (M.R.).  
Released under CC BY-NC-ND 4.0. Attribution required. Commercial use prohibited.  

> **Historical / exploratory status:** This brief belongs to an earlier physics-facing branch and is preserved as a research-design record. It is not current evidence for the framework and does not override the present retained-state selection or non-Markovian information-paths specifications.

# Verrell’s Law — Replication Brief v1.0 (Public)

**Purpose**  
Empirically test for *field-weighted collapse* signatures in legacy quantum experiments. Outcome is binary: detect pre-specified bias patterns beyond chance, or set tight upper bounds.

**Scope**  
- Bell-test archives (photons/spins), delayed-choice/quantum-eraser variants.  
- Publicly defined metrics only.  
- Full preregistration + hashing for auditability.

---

## 1) Datasets (public, suggested)
- Delft (2015) – event-ready electron spins, loophole-free.
- NIST (2015–2016) – photons, open data & reference code.
- Vienna (2015) – high-efficiency entangled photons.
- Weihs (1998) – strict locality test, raw Alice/Bob logs.
- (Optional) Quantum eraser runs (e.g., delayed-choice visibility tests).

> Use original data sources or their mirrored archives. Respect each dataset’s license/README and avoid redistributing raw data if disallowed.

---

## 2) Preregistration (required before analysis)

For each dataset, publish a short prereg doc that fixes:
- **Hypotheses** (per metric below), **alpha**, **multiple-testing correction**, **exclusion criteria** (e.g., warm-up, detector saturation).  
- **Analysis code** commit hash and environment (interpreter + libs).  
- **Random seeds** and permutation/block sizes.  
- **SHA-256** of prereg text and code bundle.

**Hash lines example**
```text
SHA256(Weihs98_Prereg_v1.txt)= <hex>
SHA256(metrics_v1_code.zip)= <hex>
Timestamp: YYYY-MM-DD HH:MM UTC
Signed by: M.R. (Verrell Moss Ross)
```

Store hashes in `/hashes/` and paste them into the prereg file and repo README.

---

## 3) Metrics

All tests preserve temporal structure (block-wise resampling) and report effect size + p + q (BH-FDR).

### M1. Coincidence-window asymmetry vs. history  
- Counts C_ab(t) for setting pair (a,b).  
- Test C_ab(t) conditioned on previous k∈{1..5} outcomes/settings vs. unconditional expectation.  
- **Stats:** log-likelihood ratio + block permutation/Bootstrap CI.

### M2. Outcome streak / after-effect  
- Probability that outcome at t repeats/anti-repeats outcome at t-1 beyond RNG-consistent null.  
- **Effect size:** Cohen’s h. **Test:** permutation with run-length preservation.

### M3. Settings ↔ outcome residual coupling  
- Residual correlation between fast RNG settings and outcomes after known bias corrections (e.g., detector efficiency).  
- **Metric:** mutual information I(settings;outcomes) vs. shuffled-block baseline.

### M4. Latency drift / wait-time bias  
- Inter-event waiting times W(t) conditioned on prior outcomes/settings.  
- **Tests:** KS/AD with block bootstrap; also report ACF/PACF.

### M5. Time-of-day / run-order modulation  
- Regress residuals vs. run index/time-of-day (GLM or harmonic regression).  
- **Correction:** BH-FDR across harmonics.

### (Optional) M6. Quantum-eraser visibility shift  
- Change in visibility ΔV when “erase” choice is space-like separated; robustness to instrumental drift.

---

## 4) A-priori decision thresholds

- Within each dataset, significance must survive **BH-FDR q ≤ 0.05** across all registered metrics.  
- **Replication requirement:** At least one metric significant (same direction) in ≥ 2 independent datasets.  
- Otherwise, publish **95% upper bounds** (effect-size caps) via test inversion.

---

## 5) Controls & robustness

- **RNG audit:** verify setting streams are independent of outcomes.  
- **Coincidence-window sensitivity:** repeat with {2,4,8,16} ns (photons) or appropriate spin-timing windows. Direction must be stable.  
- **Detector dead-time/saturation:** exclude top/bottom x% rate windows; confirm invariance.  
- **No cherry-picking:** runs/windows fixed in prereg; all deviations documented.

---

## 6) Outputs (public artifacts)

```text
/Replication_Brief_v1.0/
  README.md
  /scripts/metrics_v1/
  /results/
  /hashes/
  /FIGS/
```

Each summary should include: dataset name, N, exclusions, metrics tested, point estimates, 95% CI, p, q, robustness notes, and code hash.

---

## 7) Interpretation rule

- **Positive:** ≥1 metric meets criteria and replicates in ≥2 datasets, same direction, robustness checks passed.  
- **Null:** otherwise; report bounds (“no effect above X at 95%”).  
- Either outcome tightens the empirical picture.

---

## 8) Minimal prereg template

```text
Dataset: NIST (2015) photons — belltestdata

Hypotheses:
 H1 (M1): History-conditioned coincidence residuals > shuffled-block baseline (k=1..5).
 H2 (M2): Outcome streak bias differs from RNG-consistent null (Cohen’s h ≠ 0).
 H3 (M3): Mutual information I(settings; outcomes) > shuffled-block baseline.

Stats:
 - M1: LLR with block permutation (block = 500 ms); 10k perms.
 - M2: Cohen’s h; permutation preserving run-length distribution; 10k perms.
 - M3: MI via 10-bin equiprobable discretization; shuffled-block baseline; 10k perms.

Alpha and correction:
 alpha = 0.05; BH-FDR across H1–H3 within dataset; two-sided.

Exclusions:
 - Detector warm-up first 2 minutes (per detector log).
 - Dead-time saturation windows flagged by rate > P99.5 across the run.

Decision:
 - Positive requires ≥1 metric significant after BH and replicated in Delft or Vienna.

Hashes:
 SHA256(prereg.txt)= <hex>
 SHA256(analysis_code.zip)= <hex>
 Timestamp: YYYY-MM-DD HH:MM UTC
 Signed: M.R. (Verrell Moss Ross)
```

---

## 9) Evidence boundary

Historical terminology in this document should not be read as a current assertion that a ψμν mechanism exists. A result is relevant only if a predeclared hypothesis survives controls, held-out testing, and independent replication. Conventional quantum, instrumental, thermal, environmental, and statistical explanations must be ruled out first.

---

### Attribution

**Author / originator:** Marcos Verrell Moss Ross (M.R.)  
**Status:** Public historical replication-design note  
© 2025 Marcos Verrell Moss Ross (M.R.). All rights reserved except as granted by the CC BY-NC-ND 4.0 notice above.
