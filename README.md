# LSTM Stock Market Forecasting

A notebook-based stock-market forecasting project built around a Long
Short-Term Memory (LSTM) network. The standard workflow uses technical
indicators directly, while Principal Component Analysis (PCA) can be enabled
as an optional preprocessing step.

Suggested repository name: **`lstm-stock-market-forecasting`**

## Overview

The notebook covers the complete experiment:

```text
market data -> technical indicators -> chronological split
            -> training-only scaling -> optional PCA -> sequences -> LSTM
```

It downloads AAPL daily data by default, calculates ten technical indicators,
trains an LSTM, and evaluates the test-period forecasts against a simple
last-close baseline.

## Repository contents

```text
lstm_stock_market_forecasting.ipynb  complete experiment
requirements.txt                     Python dependencies
README.md                            project documentation
LICENSE                              MIT license
```

Generated datasets, notebook checkpoints, and trained models are excluded from
Git.

## Setup

```bash
python -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
jupyter notebook lstm_stock_market_forecasting.ipynb
```

Run the notebook from top to bottom.

## Configuration

The main experiment settings are grouped in the first code cell:

```python
TICKER = "AAPL"
START_DATE = "2015-01-01"
END_DATE = "2023-01-01"
SEQUENCE_LENGTH = 60
PCA_COMPONENTS = None
```

PCA is disabled by default. To enable it, set the number of components:

```python
PCA_COMPONENTS = 4
```

The LSTM architecture and evaluation procedure remain unchanged when PCA is
enabled.

## Evaluation design

The notebook avoids random time-series splitting. Instead, it:

- creates chronological training, validation, and test periods;
- fits feature scaling, target scaling, and optional PCA on training rows only;
- uses the validation period for early stopping;
- keeps the test period untouched until final evaluation; and
- compares the LSTM with a last-close persistence baseline.

The notebook reports MAE, RMSE, and MAPE. Results depend on the asset, period,
features, and random seed, so PCA should be treated as an option rather than an
assumed improvement.

## Background

The project originated as an exploratory experiment in January 2025 and was
later refined into the current notebook. Presentation material, stored notebook
output, and generated models are not included.

## Disclaimer

This project is intended for educational experimentation. It is not financial
advice or a trading system. Users are responsible for complying with the market
data provider's terms.

## License

MIT. See [LICENSE](LICENSE).
