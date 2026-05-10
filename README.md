# 📊 Stock Market Predictor

A machine learning web application that predicts next-day stock prices using an **LSTM Neural Network**, built with Flask and TensorFlow.

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.x-green.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)

---

## 📌 Overview

The app accepts any stock ticker symbol, fetches up to a year of historical closing prices, trains a 3-layer LSTM on the fly, and returns a next-day price prediction alongside a Buy / Hold / Avoid signal. It supports both US stocks (NYSE/NASDAQ) and Indian stocks (NSE/BSE).

---

## 👩‍💻 My Contributions

This was a team project. My specific contributions:

- **Designed and implemented the dual API fallback system** — Alpha Vantage is used as the primary data source for US stocks. If it fails (rate limit, invalid symbol, network error), the system automatically falls back to Yahoo Finance via `yfinance`, which also handles Indian stocks natively. This makes the app significantly more reliable than single-source implementations and extends coverage to NSE/BSE without any extra configuration from the user.
- **Built the Buy / Hold / Avoid signal logic** — rather than returning a raw price prediction and leaving interpretation to the user, I implemented a signal layer on top of the LSTM output. The predicted price is compared to the last known closing price: ≥2% increase signals BUY, ≤2% decrease signals AVOID, and anything within that band signals HOLD. The 2% threshold was chosen to filter noise given the model's typical RMSE range.

---

## 🚀 Features

- 🧠 **LSTM Neural Network** trained in real-time per query (3-layer, 50 units each, 20 epochs)
- 📈 **Interactive chart** showing last 120 days of prices + predicted next day
- ✅ **Buy / Hold / Avoid** signal with percentage change calculation
- 📊 **Model accuracy** estimate displayed per prediction
- 🌍 Supports **US stocks** (NYSE/NASDAQ) and **Indian stocks** (NSE/BSE via `.NS`/`.BO` suffix)
- 🔁 **Dual data source:** Alpha Vantage (primary) → Yahoo Finance (automatic fallback)
- 💡 Quick-access buttons for 9 popular stocks

---

## 🧠 How It Works

1. **Data Fetching** — Alpha Vantage for US stocks; auto-fallback to yfinance on failure or for Indian stocks
2. **Preprocessing** — MinMaxScaler normalisation, 60-day lookback sequences, 80/20 train/test split
3. **LSTM Training** — 3-layer LSTM (50 units each), 20 epochs, batch size 32, trained per request
4. **Prediction** — Final 60-day window fed to the trained model; inverse-transformed back to price scale
5. **Signal Logic:**
   - Predicted price **≥ 2% above** last close → ✅ BUY
   - Predicted price **≤ 2% below** last close → ❌ AVOID
   - Within ±2% → ⏳ HOLD

---

## 🖥️ Tech Stack

| Layer          | Technology                              |
| -------------- | --------------------------------------- |
| Backend        | Python, Flask                           |
| ML Model       | TensorFlow / Keras (LSTM)               |
| Data Sources   | Alpha Vantage API, Yahoo Finance (yfinance) |
| Data Processing| Pandas, NumPy, scikit-learn (MinMaxScaler) |
| Visualisation  | Matplotlib                              |
| Frontend       | HTML, CSS (custom dark theme)           |
| Deployment     | Heroku (Procfile + gunicorn)            |

---

## ⚙️ Setup

```bash
git clone https://github.com/taneesha-beep/Stock-Market-Predictor.git
cd Stock-Market-Predictor

python3 -m venv venv
source venv/bin/activate

pip install flask alpha_vantage yfinance tensorflow scikit-learn matplotlib pandas numpy gunicorn

python app.py
```

Open **http://127.0.0.1:5000**

---

## 📌 Stock Symbol Examples

| Stock               | Symbol         |
| ------------------- | -------------- |
| Apple               | `AAPL`         |
| Tesla               | `TSLA`         |
| Reliance Industries | `RELIANCE.NS`  |
| Infosys             | `INFY.NS`      |
| HDFC Bank           | `HDFCBANK.NS`  |

> Indian stocks use `.NS` for NSE and `.BO` for BSE.

---

## 📁 Project Structure

```
stock-market-predictor/
├── app.py          # Flask routes
├── model.py        # LSTM architecture, training, prediction, plotting
├── utils.py        # Data smoothing helpers
├── requirements.txt
├── Procfile        # Heroku deployment
├── templates/
│   └── index.html
└── static/
    └── style.css
```

---

## ⚠️ Disclaimer

Educational purposes only. Not financial advice. The LSTM model has inherent limitations and market movements are influenced by many factors outside the model's scope.
