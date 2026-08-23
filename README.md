# Adaptive Honeypot Deception

**Code, data generator, and experiments for the paper:**
*Adaptive Honeypot Deception for Detecting Stealthy and Human-Like Cyber Intrusions: A Behavioral-Separability Framework*
Naif Alsharabi, Talal Alshammari, Shoayee Alotaibi, Ali Alferaidi, Amr Jadi, and Habib Hamam.

This repository reproduces **every number, table, and figure** reported in the paper. It contains an event-level session simulator with an attacker realism continuum, a 19-feature behavioral analytics pipeline, the Behavioral Separability Index (BSI) with its detectability bounds, and the full experimental campaign (realism sweep, hard negatives, leave-one-strategy-out, sequential early detection, calibration, imbalance/noise robustness, and evasion-cost analysis).

---

## Highlights

- **Attacker realism continuum.** A mimicry operator `M_λ(θ) = (1−λ)·θ_mal + λ·θ_norm` interpolates attacker behavior from naive automation (λ = 0) to human-like mimicry (λ = 1), instantiated as five profiles A0–A4.
- **Behavioral Separability Index.** Mean Jensen–Shannon divergence between legitimate and attack feature distributions, with provable distribution-free bounds on the error of *any* detector — verified empirically at every λ.
- **Sequential early detection.** Per-event posterior risk with a stopping rule: median attack detected after **3 events**, 85.9% before the first honey file is touched.
- **Operationally honest evaluation.** Six hard-negative legitimate scenarios (0.0% FPR), attack prevalence down to 0.5%, telemetry corruption up to 30%, probability calibration (isotonic ECE = 0.006), and an evasion–yield trade-off (full mimicry cuts attacker reconnaissance yield 15×).

## Key result

Detection performance is governed by behavioral separability, not classifier choice: F1 degrades monotonically from **1.000** (λ = 0, the classical non-overlapping setting where even logistic regression is perfect) to **0.806** (λ = 1), tracking the BSI (0.32 → 0.07) and always remaining within the proven detectability ceiling.

---

## Repository structure

```
.
├── Adaptive_Honeypot_Deception_Notebook.ipynb   # Exhaustive executed notebook (start here)
├── code/
│   ├── simgen.py             # Event-level session generator (users, hard negatives, A0–A4, mimicry operator)
│   ├── experiments.py        # Full experimental campaign E1–E12
│   ├── theory_analyses.py    # Bound verification, early-warning score, evasion cost
│   └── figures.py            # Publication figures
├── Outputs/
│   └── Adaptive_Honeypot_Deception/
│       ├── Data/Generated/   # Generated datasets (easy + main, CSV)
│       ├── Tables/           # All result tables (CSV)
│       ├── Figures/          # All figures (PNG)
│       └── Outputs_Summary.txt
└── README.md
```

## Quick start

### Option 1 — Notebook (recommended)

Open `Adaptive_Honeypot_Deception_Notebook.ipynb` locally or in Google Colab and *Run all*. The notebook is fully self-contained (no imports from `code/`), organized in 25 modules mirroring the paper's experiments, and writes all outputs to `Outputs/` (or `MyDrive/Outputs/` on Colab).

Runtime: ~15–25 minutes on a standard CPU.

### Option 2 — Scripts

```bash
pip install numpy pandas scipy scikit-learn matplotlib
python code/experiments.py       # full campaign E1–E12
python code/theory_analyses.py   # bound verification, EWS, evasion cost
python code/figures.py           # publication figures
```

## Reproducibility

All random seeds are fixed; a complete run reproduces the paper's reported values exactly, including:

| Quantity | Value |
|---|---|
| BSI (easy / main dataset) | 0.444 / 0.166 |
| F1 across realism sweep (λ = 0 → 1) | 1.000 → 0.806 |
| Recall on human-like profile A4 (holdout / unseen) | 0.605 / 0.490 |
| Median time-to-detection | 3 events |
| Detected before first honey-file access | 85.9% |
| Calibration ECE (isotonic) | 0.0065 |
| Attacker yield-rate collapse under full mimicry | 15× |

Tested with Python 3.11 and scikit-learn 1.x; minor version differences may shift third decimals.

## Citation

If you use this code, please cite the paper:

```bibtex
@article{alsharabi2026adaptive,
  title   = {Adaptive Honeypot Deception for Detecting Stealthy and Human-Like
             Cyber Intrusions: A Behavioral-Separability Framework},
  author  = {Alsharabi, Naif and Alshammari, Talal and Alotaibi, Shoayee and
             Alferaidi, Ali and Jadi, Amr and Hamam, Habib},
  year    = {2026},
  note    = {Under review}
}
```

## License

Released under the MIT License (see `LICENSE`).

## Contact

Corresponding author: Naif Alsharabi — n.sharabi@uoh.edu.sa

## Acknowledgment

This research was funded by the Scientific Research Deanship at the University of Ha'il, Saudi Arabia, under project number RG-25 013.
