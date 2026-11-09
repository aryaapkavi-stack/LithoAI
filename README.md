# LithoAI 2.0
### Machine Learning for Semiconductor Manufacturing Defect Prediction

LithoAI 2.0 is an experimental research project investigating the use of machine learning for defect prediction and process monitoring in semiconductor manufacturing.

Using the UCI SECOM dataset, this study examines the challenges of high-dimensional sensor data, class imbalance, missing measurements and temporal changes in manufacturing data.

The focus is not only on predictive performance, but also on evaluating model reliability, validation strategies and the trade-offs between failure detection and inspection workload.

## Research objectives

- Evaluate machine learning models for semiconductor manufacturing defect prediction.
- Study model performance under severe class imbalance.
- Investigate robustness to additional missing sensor readings.
- Examine generalisation across chronological data partitions.
- Analyse sensor-level distribution and missingness changes.
- Evaluate the practical trade-off between recall, precision and inspection workload.

## Dataset

The project uses the **UCI SECOM semiconductor manufacturing dataset**.

| Characteristic | Value |
|---|---:|
| Observations | 1,567 |
| Sensor features | 590 |
| Failed observations | 104 |
| Passing observations | 1,463 |
| Failure prevalence | 6.64% |
| Unique timestamps | 1,534 |

The dataset contains substantial missing sensor measurements, repeated timestamps and low-variation features.

[UCI SECOM dataset](https://archive.ics.uci.edu/static/public/179/secom.zip)

## Methodology

The experimental workflow includes:

1. **Data exploration:** Missing-value analysis, timestamp inspection and feature-quality checks.
2. **Preprocessing:** Sensor filtering, imputation and model pipelines.
3. **Grouped validation:** Five-fold StratifiedGroupKFold evaluation using timestamp groups.
4. **Model comparison:** Logistic Regression, Random Forest and HistGradientBoosting.
5. **Nested threshold evaluation:** Five outer folds and four inner folds, using an illustrative 80% recall target.
6. **Missing-data robustness:** Five repetitions with 0%, 5%, 10%, 20% and 30% additional test-time missingness.
7. **Temporal evaluation:** Expanding-window validation across later chronological periods.
8. **Sensor analysis:** Distribution shifts, missingness changes and grouped permutation importance.

## Selected experimental results

### 1. Grouped cross-validation

Pooled out-of-fold average precision (AP):

| Model | AP |
|---|---:|
| Logistic Regression | 0.1390 |
| Random Forest | 0.1926 |
| HistGradientBoosting | 0.1880 |

The overall failure-prevalence baseline was 0.0664. Both tree-based models performed above this baseline, although performance varied across folds.

### 2. Nested threshold evaluation

Thresholds were selected within the inner grouped folds and evaluated on untouched outer folds.

| Model | Recall | Precision | Inspection rate |
|---|---:|---:|---:|
| Random Forest | 76.92% | 11.19% | 45.63% |
| HistGradientBoosting | 82.69% | 9.46% | 58.01% |

HistGradientBoosting detected more failures, but required a higher inspection workload. These results illustrate why recall should not be considered in isolation.

### 3. Robustness to additional missing data

Comparison between 0% and 30% additional test-time missingness:

| Model | AP (0% → 30%) | Recall (0% → 30%) |
|---|---:|---:|
| HistGradientBoosting | 0.2289 → 0.1994 | 82.82% → 75.24% |
| Random Forest | 0.2279 → 0.2072 | 77.45% → 87.96% |

Random Forest's higher recall at 30% missingness came with an increase in inspection rate from 45.66% to 64.38%. The models therefore showed different responses to sensor-data loss.

### 4. Chronological generalisation

Expanding-window validation produced the following AP scores:

| Test period | Random Forest | HistGradientBoosting |
|---|---:|---:|
| Period 3 | 0.2795 | 0.2979 |
| Period 4 | 0.0579 | 0.0471 |
| Period 5 | 0.0930 | 0.0543 |
| Mean across periods | 0.1435 | 0.1331 |

The later periods contained only 11, 11 and 17 failures, respectively. Results should therefore be interpreted cautiously. The decline in performance does not establish a causal relationship with sensor drift.

### 5. Sensor distribution analysis

The chronological sensor audit found an increase in the number of sensors with median shifts greater than one training IQR:

- Period 3: 1 sensor
- Period 4: 7 sensors
- Period 5: 9 sensors

The number of sensors with missingness changes exceeding 10 percentage points also increased across the evaluated periods. These are descriptive indicators of temporal data changes, not proof of their cause or impact on model performance.

## Key observations

- Timestamp-grouped validation is important for avoiding overlap between observations sharing timestamps.
- Tree-based models achieved higher pooled AP than Logistic Regression in the grouped evaluation.
- Higher failure recall can require substantially more inspections.
- Additional missingness affected the models differently.
- Predictive performance varied considerably across chronological periods.
- Missingness indicators did not provide a consistent improvement across the three temporal test periods.

## Limitations

- The study uses a single public dataset with only 104 failure observations.
- The chronological test periods contain relatively few failures.
- SECOM is a general semiconductor manufacturing dataset; it does not establish lithography-specific predictive performance.
- Artificial sensor masking does not necessarily reproduce real industrial missing-data mechanisms.
- Sensor importance and distribution shifts are exploratory and should not be interpreted causally.
- No production deployment or external manufacturing-line validation has been conducted.

## Repository structure

```text
LithoAI/
├── notebooks/
│   ├── documentation/
│   ├── results/
│   ├── LithoAI_2_0_Audited_Cleaned (1).ipynb
│   ├── lithoai_experiments.ipynb
│   └── README.md
├── .gitignore
├── requirements.txt
└── README.md
```

## Tools and technologies

- Python
- NumPy and Pandas
- Scikit-learn
- Matplotlib and Seaborn
- Google Colab
- Git and GitHub

## Reproducibility

The research notebook downloads the UCI SECOM dataset directly from its archive. It is designed to run in Google Colab.

Install the listed dependencies using:

```bash
pip install -r requirements.txt
```

Run the notebook from top to bottom to reproduce the experiments. Random seeds and validation procedures are specified in the notebook.

## Future work

- Further investigate temporal generalisation.
- Explore sensor stability and feature relationships.
- Evaluate additional model and threshold-selection strategies.
- Test on independent semiconductor manufacturing datasets.
- Investigate the feasibility of adapting the framework to more specific manufacturing processes.

## Author

**Aryaa Kavi**  
B.Tech — VLSI Design and Technology

An ongoing independent research project exploring machine learning methods for semiconductor manufacturing analysis.
