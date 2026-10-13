# Multimodal Overflow Risk Simulation

A simulation study comparing fixed-weight fusion, heuristic adaptive-weight fusion, machine-learning models, and ToF-based baselines for liquid-overflow risk estimation during heating.

## Overview

This project investigates how acoustic, time-of-flight (ToF) liquid-height, temperature, and ambient-humidity features can be combined to estimate liquid-overflow risk.

Six methods are evaluated using synthetic heating-cycle data:

1. Fixed-weight fusion (equal weights)
2. Adaptive-weight fusion (heuristic)
3. Logistic regression
4. Gradient boosting
5. ToF-only detection
6. ToF with rate-of-change detection

The system is designed to generate audio-visual warnings only. It does not automatically control or switch off the cooking appliance.

## Research Objectives

- Compare multimodal fusion strategies for overflow-risk estimation.
- Evaluate event detection, false alarms, and warning lead time.
- Investigate the contribution of individual sensor modalities through ablation experiments.
- Examine robustness under increased sensor noise and sensor dropout.
- Provide a reproducible simulation-based evaluation framework.

## Methodology

The simulation uses four normalized risk features:

- Acoustic feature: simulated peak frequency.
- Liquid-height feature: simulated ToF distance.
- Temperature feature: simulated temperature in °C.
- Humidity feature: simulated relative humidity.

Each simulated dataset contains 1,000 heating cycles of 360 seconds, sampled at 1 Hz. Ten independent seeds (1000–1009) are used.

Each dataset is split by complete cycle into:
- Training: 600 cycles
- Validation: 200 cycles
- Testing: 200 cycles

Learned model parameters are fitted on training data. Warning thresholds are selected on validation data using a predefined false-alarm constraint. Final performance is reported on held-out test cycles.

## Results Summary

Under the synthetic simulation conditions:

- Adaptive fusion achieved a mean detection rate of 99.9%.
- Fixed-weight fusion achieved a mean detection rate of 97.9%.
- ToF-only detection achieved a mean detection rate of 66.1%.
- Gradient boosting achieved a mean warning lead time of 27.2 seconds, with a lower detection rate of 79.0%.
- Ablation experiments indicated that the simulated acoustic feature contributed substantially to detection performance.

Results are averages across ten seeds. Refer to the CSV files and research manuscript for detailed metrics, confidence intervals, robustness experiments, and statistical comparisons.

## Repository Contents

- `overflow_simulation_study.py` — simulation and evaluation implementation.
- `results_log.txt` — experiment output summary.
- `per_seed_results.csv` — results for individual seeds.
- `table_main.csv` — main comparison results.
- `table_ablation.csv` — modality-ablation results.
- `table_robustness.csv` — robustness-test results.
- `table_paired_tests.csv` — paired statistical comparisons.
- `logistic_coefficients.csv` — logistic regression coefficients.
- `fig_tradeoff_curves.png` — detection and lead-time trade-off plots.

## Requirements

Python 3 and the following packages are used:

- NumPy
- pandas
- SciPy
- scikit-learn
- Matplotlib

Install dependencies using:

```bash
pip install numpy pandas scipy scikit-learn matplotlib
```

## Running the Simulation

Run the following command from the repository directory:

```bash
python overflow_simulation_study.py --seeds 10 --out results
```

The script is intended to regenerate the simulation outputs for seeds 1000–1009. Verify the generated files against the committed results when reproducing the experiments.

## Limitations

All sensor readings and overflow labels in this project are synthetic. The generator uses predefined mathematical patterns and does not represent a physically calibrated model of boiling or overflow.

The results do not establish the performance of a real cooking device. Physical sensor measurements and experiments under representative household cooking conditions are required before practical effectiveness can be assessed.

## Citation

If you use this work, cite the associated research manuscript:

*Fixed vs. Adaptive Weighting for Multimodal Liquid-Overflow Risk Estimation: A Simulation Study.*

A complete citation can be added after publication.

## License

Add a license file before permitting others to reuse or redistribute this code.
