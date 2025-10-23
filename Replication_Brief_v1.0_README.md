© 2025 M.R. (Inappropriate Media Ltd / Collapse Aware AI).  
Released under CC BY-NC-ND 4.0. Attribution required. Commercial use prohibited.  

# Verrell’s Law — Replication Brief v1.0 (Public)

**Purpose**  
Empirically test for *field-weighted collapse* signatures in legacy quantum experiments **without** exposing any proprietary ψμν constants or governor logic. Outcome is binary: detect pre-specified bias patterns beyond chance, or set tight upper bounds.

**Scope**  
- Bell-test archives (photons/spins), delayed-choice/quantum-eraser variants.  
- ψμν-agnostic metrics only (dimensionless statistics; no private parameters).  
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
```
SHA256(Weihs98_Prereg_v1.txt)= <hex>
SHA256(metrics_v1_code.zip)= <hex>
Timestamp: YYYY-MM-DD HH:MM UTC
Signed by: M.R. (Verrell Moss Ross)
```

Store hashes in `/hashes/` and paste them into the prereg file and repo README.

---

## 3) Metrics (ψμν-agnostic)

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

```
/Replication_Brief_v1.0/
  README.md                 <-- this file
  /scripts/metrics_v1/      <-- dataset-agnostic code
  /results/
    /weihs1998/summary.json
    /nist2015/summary.json
    /vienna2015/summary.json
    /delft2015/summary.json
  /hashes/
    prereg_shas.txt
    code_shas.txt
  /FIGS/
    <minimal plots only>
```

Each summary.json must include: dataset name, N, exclusions, metrics tested, point estimates (effect sizes), 95% CI, p, q, robustness notes, code hash.

---

## 7) Interpretation rule

- **Positive:** ≥1 metric meets criteria and replicates in ≥2 datasets, same direction, robustness checks passed.  
- **Null:** otherwise; report bounds (“no effect above X at 95%”).  
- Either outcome tightens the empirical picture: confirmation or constraint.

---

## 8) Minimal prereg template (copy/paste)

```
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

Robustness:
 - Coincidence window = {2, 4, 8, 16} ns; effect direction must be stable.

Decision:
 - Positive requires ≥1 metric significant after BH and replicated in Delft or Vienna.

Environment:
 - Python 3.x / R x.y; list exact libs + versions.
 - Fixed random seed(s).

Hashes:
 SHA256(prereg.txt)= <hex>
 SHA256(analysis_code.zip)= <hex>
 Timestamp: YYYY-MM-DD HH:MM UTC
 Signed: M.R. (Verrell Moss Ross)
```

---

## 9) Empirical Test Addendum (Perplexity Alignment)

To standardize external replication, the following procedures are recognized as **equivalent** to the metrics above:

1. **Coincidence Bias Analysis**  
   Compute conditional probabilities P(o_a,o_b | s_a,s_b,k) for successive histories k. Deviations from Born-rule expectations = candidate ψμν bias.  
   *(Equivalent to M1; conditional Born-rule deviation test).*

2. **Latency Drift Assessment**  
   Autocorrelation + partial autocorrelation (ACF/PACF) and clustering (e.g., DBSCAN) on inter-event latencies Δt.  
   *(Extends M4 with explicit time-series diagnostics).*

3. **Collapse Asymmetry Detection**  
   Symmetry-residual tests under parameter flips/apparatus re-orientation; run-length and geometric cluster analyses.  
   *(Covers M2 + M3 under symmetry framing).*

4. **Field-Weighted Correlation Residuals**  
   Apply context weighting w=f(E,B,∇I) to outcome residuals; evaluate coherence with predicted gradients via correlation tests and **Bayes Factors** (below).  
   *(Vocabulary alignment; does not reveal proprietary f(·)).*

5. **Cross-Validation**  
   Repeat across Weihs ’98, Delft ’15, Vienna ’15, NIST ’15 to rule out dataset-specific artifacts.  
   *(Matches the replication requirement).*

### Bayes-factor model comparison (optional)
Compare ψμν-weighted vs. null (standard quantum) models using Bayes Factor B_10.  
- Prior on ψμν-weight parameters: broad, zero-centered, truncated to respect physical bounds (no proprietary constants).  
- Interpretation (Jeffreys): B_10>3 = positive; >10 = strong evidence.  
- Report sensitivity to prior width; include robustness plots.

**Note:** This section is optional and ψμν-agnostic; do **not** disclose private kernels or governor mappings.

---

## 10) Compliance & privacy

- No numeric ψμν constants, kernels, or governor transfer functions are ever published.  
- All public scripts are dataset-agnostic; all sensitive IP stays in the private Solace/EchoGuard environment and with the verified developer under NDA.

---

### Attribution & Protection

**Author:** M.R. (Verrell Moss Ross)  
**Affiliation:** Inappropriate Media Limited (t/a Collapse Aware AI)  
**Protection:** Verrell-Solace Sovereignty Protocol. Intellectual and Emergent Rights Reserved.  
© 2025 All Rights Reserved.

**Motto:** Transparency of method, protection of mechanism.
