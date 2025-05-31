# GT-XGBoost: Google Trends-Augmented XGBoost for Market Volatility Prediction

[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This repository contains the implementation for **"Google Trends–Augmented XGBoost for Market Volatility Prediction: A Machine–Learning Early-Warning System"**. GT-XGBoost integrates behavioral sentiment indicators from Google search data with traditional volatility measures to predict VIX spikes with superior performance compared to established academic benchmarks.

**Key Results**: ROC AUC of 0.796, ranking #1 among 8 academic benchmarks with 65.4% precision and 58.6% recall for 1-month ahead VIX spike prediction.

## Installation

```bash
git clone https://github.com/yourusername/GT-XGBoost.git
cd GT-XGBoost
pip install -r requirements.txt
```

## Quick Start

```python
from gt_xgboost import GTXGBoostPredictor
import pandas as pd

# Load data
vix_data = pd.read_csv('data/vix_data.csv')
trends_data = pd.read_csv('data/google_trends.csv')

# Train model
predictor = GTXGBoostPredictor(vix_threshold=30, random_state=42)
predictor.fit(vix_data, trends_data)

# Generate predictions
predictions = predictor.predict_volatility_spikes(horizon_months=1)
print(f"Warning level: {predictions['warning_level']}")
```



## Methodology

GT-XGBoost combines:
- **Behavioral Features**: Google Trends momentum, acceleration, and composite sentiment indices
- **Technical Features**: VIX momentum, rolling statistics, and technical indicators  
- **Hybrid Integration**: Cross-modal interaction terms and risk scoring systems

**Target**: VIX ≥ 30 spikes with 1-3 month prediction horizons

## Benchmark Results

| Model | ROC AUC | Model Type |
|-------|---------|------------|
| **GT-XGBoost** | **0.796** | **Behavioral ML** |
| Persistence | 0.788 | Traditional |
| Realized Volatility | 0.745 | Financial Engineering |
| Heston-inspired SV | 0.733 | Stochastic Volatility |
| GARCH(1,1) | 0.651 | Classical Econometric |

## Replication

```bash
# Download data
python scripts/download_data.py --start-date 2004-01-01 --end-date 2024-12-31

# Train model
python scripts/train_model.py --config configs/optimal_params.yaml

# Run benchmarks
python scripts/benchmark_comparison.py --output results/benchmark_results.csv
```

## Data Sources

- **VIX**: CBOE Volatility Index (2000-2024)
- **Google Trends**: Search volumes for "recession", "financial crisis", "volatility", "stock market crash" (2004-2024)
- **Gold Futures**: CME data for economic validation (2001-2020)

## Requirements

```
pandas>=2.2.0
numpy>=1.26.0
scikit-learn>=1.5.0
xgboost>=2.0.0
arch>=7.2.0
matplotlib>=3.7.0
```



## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Disclaimer**: This software is for research purposes only. Not intended as financial advice.
