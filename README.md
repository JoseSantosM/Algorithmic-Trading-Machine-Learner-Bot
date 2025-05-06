


# Algorithmic Trading — Predictive Trading System Using LSTM

## Overview

**Algorithmic Trading** is a predictive analytics system designed to forecast profitable Bitcoin trading opportunities using Long Short-Term Memory (LSTM) neural networks. The system utilizes historical OHLCV (Open, High, Low, Close, Volume) data, performs feature engineering, and evaluates trading strategies through backtesting.

This project follows a microservices architecture. Each component is implemented in Python using class-based structures and does not exceed 250 lines of code. The project runs entirely within a virtual environment.

---

## System Architecture

The project is composed of the following services:

### 1. Data Collection

A service that connects to a financial data provider (e.g., Binance or Yahoo Finance) to retrieve historical Bitcoin OHLCV data.

* Input: API credentials or configuration
* Output: Raw data (CSV or DataFrame) with fields: `open`, `high`, `low`, `close`, `volume`

### 2. Feature Engineering

A processing service that generates between 10 and 20 technical indicators and features from the raw data, such as:

* Price spreads: `high - close`, `close - open`
* Technical indicators: Moving Averages, RSI, MACD
* Volume-based features
* Normalization and scaling

Features are validated using backtesting metrics to ensure their predictive relevance.

### 3. Model Training

An LSTM-based neural network model is trained using:

* 80% of the dataset for training
* 20% for validation/testing
* Input: Engineered features
* Output: Predicted class (e.g., buy/sell/hold)

### 4. Prediction and Evaluation

This module uses the trained model to generate trading signals and assesses model performance using a backtesting library. Metrics such as cumulative return, drawdown, and precision are used to evaluate the effectiveness of the strategy.

### 5. Decision Making (Buy, Sell, or Hold)

Based on the predictions from the LSTM model, a decision-making function will determine the optimal time to buy, sell, or hold. This is done by evaluating the model's predicted class at each time step and taking the following actions:

* **Buy Signal**: When the model predicts that the Bitcoin price will increase, the system issues a "buy" signal.

  * **Condition**: If the model's output predicts that the next price point will be higher than the current price.
  * **Action**: Buy Bitcoin to capture the upcoming price increase.

* **Sell Signal**: When the model predicts that the Bitcoin price will decrease, the system issues a "sell" signal.

  * **Condition**: If the model's output predicts that the next price point will be lower than the current price.
  * **Action**: Sell Bitcoin to avoid the expected loss from a price decline.

* **Hold Signal**: When the model predicts little to no price movement, the system issues a "hold" signal.

  * **Condition**: If the model's output predicts that the next price point will remain similar to the current price.
  * **Action**: Do nothing and hold onto the current position.

This decision-making logic is integrated into the prediction module and ensures that trades are only executed when a profitable opportunity is forecasted.

---

## Technology Stack

* Python 3.10+
* TensorFlow / Keras
* Pandas, NumPy
* Scikit-learn
* Matplotlib / Seaborn
* Backtesting framework (e.g., Backtrader)
* Financial data API (e.g., Binance, Yahoo Finance)

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/JoseSantosM/Algorithmic-Trading-Machine-Learner-Bot.git
cd Algorithmic-Trading-Machine-Learner-Bot
```

### 2. Create and Activate a Virtual Environment

```bash
python -m venv env
source env/bin/activate  # On Windows: env\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Project Structure

```
tradeflow/
│
├── data_collector/
│   └── collector.py            # Downloads and stores OHLCV data
│
├── feature_engineering/
│   └── engineer.py             # Generates and validates features
│
├── model/
│   └── lstm_model.py           # Defines and trains the LSTM model
│
├── decision_maker/
│   └── decision.py             # Determines buy, sell, or hold signals based on model predictions
│
├── evaluation/
│   └── backtest.py             # Performs backtesting and evaluation
│
├── requirements.txt            # Python dependencies
├── README.md                   # Project documentation
└── .env                        # Environment configuration (optional)
```

---

## Development Guidelines

* Each script must remain under **250 lines of code**
* All code must follow a **class-based structure**
* The entire project must run in a **Python virtual environment**
* All dependencies must be listed in `requirements.txt`
* The system uses **Bitcoin OHLCV data only**
* Time series frequency (e.g., hourly or daily candles) must be consistent and specified
* Project progress is reviewed every **Tuesday and Friday**

---
