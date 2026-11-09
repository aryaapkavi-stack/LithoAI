# LithoAI 2.0
### Exploring Machine Learning for Semiconductor Manufacturing Process Monitoring

## Overview

LithoAI 2.0 is an experimental research project investigating how machine learning can support failure prediction and process monitoring in semiconductor manufacturing.

The project uses the SECOM semiconductor manufacturing dataset to explore the challenges of working with high-dimensional sensor data, class imbalance, missing measurements and changes in data distributions over time.

Rather than focusing only on predictive accuracy, the project also examines model reliability, validation strategies and the practical trade-offs involved in identifying potentially failing manufacturing processes.

## Research Objectives

- Investigate machine learning approaches for semiconductor manufacturing failure prediction.
- Evaluate model performance under significant class imbalance.
- Examine the effect of missing sensor measurements on predictive reliability.
- Study model generalisation across chronological data splits.
- Explore sensor-level distribution changes and their potential implications for process monitoring.

## Dataset

The project uses the SECOM dataset, which contains semiconductor manufacturing process measurements.

Key characteristics include:
- 1,567 observations
- 590 sensor features
- Highly imbalanced failure labels
- Significant missing sensor measurements

The dataset presents challenges commonly encountered in industrial sensor-data analysis.

## Methodology

The experimental workflow includes:

1. **Data exploration and preprocessing** – examining missing values, feature distributions and class imbalance.
2. **Model development** – evaluating Logistic Regression, Random Forest and HistGradientBoosting.
3. **Model evaluation** – using precision-recall metrics and grouped cross-validation.
4. **Threshold analysis** – examining the trade-off between failure detection and inspection workload.
5. **Missing-data robustness** – testing model behaviour under simulated increases in missing sensor measurements.
6. **Temporal evaluation** – investigating generalisation across chronological data partitions.
7. **Sensor distribution analysis** – examining changes in sensor behaviour across time periods.

## Current Research Status

The project is in the experimental evaluation and validation stage.

Current work focuses on:
- Comparing model performance under appropriate validation strategies.
- Evaluating robustness to missing measurements.
- Investigating temporal generalisation.
- Identifying methodological limitations and opportunities for improvement.

Quantitative findings will be documented after the final reproducibility review.

## Tools and Technologies

- Python
- NumPy and Pandas
- Scikit-learn
- Matplotlib and Seaborn
- Google Colab
- Git and GitHub

## Limitations

The SECOM dataset is a general semiconductor manufacturing dataset. It does not, by itself, establish lithography-specific predictive performance.

The experiments are conducted on a limited dataset and should not be interpreted as evidence of production-ready deployment. Further validation on additional manufacturing datasets would be necessary.

## Future Work

- Improve experimental reproducibility.
- Investigate additional validation strategies.
- Explore feature stability and sensor relationships.
- Evaluate generalisation across additional datasets.
- Investigate the feasibility of applying the framework to more specific semiconductor manufacturing processes.

## Repository Structure

```text
LithoAI/
├── notebooks/
└── README.md
```

## Author

**Aryaa Kavi**  
B.Tech – VLSI Design and Technology

This project is an ongoing independent exploration of machine learning methods for semiconductor manufacturing analysis.
B.Tech – VLSI Design and Technology
