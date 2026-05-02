# 📊 Stock Market Predictor

A machine learning web application that predicts next-day stock prices using an **LSTM (Long Short-Term Memory) Neural Network**, built with Flask and TensorFlow.

![Python](https://img.shields.io/badge/Python-3.9+-blue.svg)
![Flask](https://img.shields.io/badge/Flask-3.x-green.svg)
![TensorFlow](https://img.shields.io/badge/TensorFlow-2.x-orange.svg)
![License](https://img.shields.io/badge/License-MIT-yellow.svg)

---

## 🚀 Features

- 🧠 **LSTM Neural Network** trained in real-time for each stock query
- 📈 **Interactive chart** showing last 120 days of prices + predicted next day
- ✅ **Buy / Hold / Avoid** suggestion based on predicted price movement
- 📊 **Model accuracy** displayed for every prediction
- 🌍 Supports **US stocks** (NYSE/NASDAQ) and **Indian stocks** (NSE/BSE)
- 💡 Quick-access buttons for 9 popular stocks
- 🔁 Dual data source: **Alpha Vantage API** with **Yahoo Finance** fallback

---

## 🖥️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Python, Flask |
| ML Model | TensorFlow / Keras (LSTM) |
| Data Sources | Alpha Vantage API, Yahoo Finance (`yfinance`) |
| Data Processing | Pandas, NumPy, Scikit-learn |
| Visualization | Matplotlib |
| Frontend | HTML, CSS (custom dark theme) |
| Deployment | Heroku (via `Procfile` + `gunicorn`) |

---

## 📁 Project Structure

```
stock-market-predictor/
├── app.py                  # Flask app & routes
├── model.py                # LSTM model, prediction logic, plotting
├── utils.py                # Helper utilities (data smoothing)
├── requirements.txt        # Python dependencies
├── Procfile                # Heroku deployment config
├── runtime.txt             # Python runtime version (for Heroku)
├── templates/
│   └── index.html          # Main UI template
├── static/
│   └── style.css           # Dark theme stylesheet
└── tests/
    └── test_app.py         # Test suite
```

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.9 or higher
- pip

### 1. Clone the repository

```bash
git clone https://github.com/your-username/stock-market-predictor.git
cd stock-market-predictor
```

### 2. Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate        # Mac/Linux
venv\Scripts\activate           # Windows
```

### 3. Install dependencies

```bash
pip install flask alpha_vantage yfinance tensorflow scikit-learn matplotlib pandas numpy gunicorn requests python-dotenv pytest
```

### 4. Run the app

```bash
python app.py
```

### 5. Open in browser

```
http://127.0.0.1:5000
```

---

## 📌 How to Use

1. Enter any valid stock symbol in the input box (e.g., `AAPL`, `TSLA`, `INFY.NS`)
2. Click **Predict**
3. Wait ~30–60 seconds while the LSTM model trains
4. View the predicted price, model accuracy, buy/sell suggestion, and trend chart

### Stock Symbol Examples

| Stock | Symbol |
|---|---|
| Apple | `AAPL` |
| Tesla | `TSLA` |
| Google | `GOOGL` |
| Reliance Industries | `RELIANCE.NS` |
| Infosys | `INFY.NS` |
| HDFC Bank | `HDFCBANK.NS` |
| Tata Motors | `TATAMOTORS.NS` |

> **Tip:** Indian stocks use `.NS` suffix for NSE and `.BO` suffix for BSE.

---

## 🧠 How It Works

1. **Data Fetching** — Pulls historical closing prices via Alpha Vantage (US stocks) or Yahoo Finance (fallback + Indian stocks)
2. **Preprocessing** — Data is normalized using MinMaxScaler and split into 60-day sequences
3. **LSTM Training** — A 3-layer LSTM model is trained on 80% of the data with 20 epochs
4. **Prediction** — The model predicts the next day's closing price
5. **Suggestion Logic:**
   - Price predicted **≥ 2% higher** → ✅ BUY
   - Price predicted **≤ 2% lower** → ❌ AVOID
   - Otherwise → ⏳ HOLD / WAIT

---

## ⚠️ Disclaimer

This project is for **educational purposes only**. Stock predictions made by this app should **not** be used as financial advice. The model has inherent limitations and market movements are influenced by many unpredictable factors.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
