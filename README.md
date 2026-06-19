# 🛒 Retail Demand Forecasting — Rossmann Store Sales

An end-to-end machine learning project that forecasts daily store-level sales for the **Rossmann drug store chain**, using historical sales, promotions, holidays, and store metadata. The project covers the full ML pipeline — data preprocessing, exploratory data analysis, feature engineering, model building, and evaluation — and is presented through an **interactive Streamlit dashboard** for business-friendly exploration.

---

## 📌 Project Overview

Retailers lose revenue every year due to poor demand forecasting — either overstocking (wasted inventory, storage costs) or understocking (missed sales, stockouts). This project builds a demand forecasting system that predicts future daily sales for individual Rossmann stores, enabling smarter inventory planning and promotional strategy.

The solution is built on the **Rossmann Store Sales dataset** (Kaggle), which contains historical sales data for 1,115 Rossmann stores across Germany, along with store attributes (type, assortment, competition) and promotional calendars.

---

## 🎯 Objectives

- Predict daily sales for each store up to several weeks in advance
- Quantify the impact of promotions on sales performance
- Identify seasonal and holiday-driven demand patterns
- Translate forecasts into actionable inventory recommendations
- Present results through an interactive, non-technical dashboard

---

## 🗂️ Dataset

**Source:** [Rossmann Store Sales – Kaggle](https://www.kaggle.com/competitions/rossmann-store-sales)

| File | Description |
|---|---|
| `train.csv` | Historical daily sales data per store |
| `store.csv` | Store metadata (type, assortment, competition distance, Promo2 details) |
| `test.csv` | Holdout data for forecast validation |

**Key fields:** `Store`, `Date`, `Sales`, `Customers`, `Open`, `Promo`, `StateHoliday`, `SchoolHoliday`, `StoreType`, `Assortment`, `CompetitionDistance`, `Promo2`.

---

## 🧹 Data Preprocessing

- Handled missing values in `CompetitionDistance`, `CompetitionOpenSinceYear/Month`, and `Promo2SinceYear/Week`
- Converted date fields into structured time features (year, month, day, week of year, day of week)
- Filtered out closed-store records (`Open == 0`) to avoid skewing the target variable
- Merged store metadata with daily sales records into a unified modeling dataset

---

## 🔍 Exploratory Data Analysis (EDA)

- Sales trends over time across stores and store types
- Seasonality patterns (monthly, weekly, day-of-week effects)
- Impact of promotions (`Promo`, `Promo2`) on average sales and customer counts
- Effect of state/school holidays on demand
- Store-type and assortment-level sales comparisons
- Correlation analysis between customers, promotions, and sales

---

## 🛠️ Feature Engineering

To improve model performance, the following engineered features were created:

- **Lag features** — sales from previous days/weeks to capture momentum
- **Rolling statistics** — rolling mean/std of sales over configurable windows
- **Promo2 flags** — whether a store is currently in an active Promo2 cycle
- **Competition duration** — time elapsed since a competitor opened nearby
- **Calendar features** — day of week, month, year, week of year, holiday flags

---

## 🤖 Models Built

Multiple models were trained and benchmarked to find the best forecasting approach:

| Model | Purpose |
|---|---|
| Baseline (mean/last-value) | Reference benchmark |
| Linear Regression | Simple interpretable baseline |
| Random Forest Regressor | Captures non-linear relationships |
| **XGBoost Regressor** | Best-performing model — final recommended model |
| LSTM (demo) | Sequence-based deep learning approach for time-series patterns |

**Evaluation metric:** RMSPE (Root Mean Squared Percentage Error) — chosen because it weighs proportional accuracy across stores with very different sales volumes.

**Result:** XGBoost delivered the strongest balance of accuracy, training speed, and interpretability (via feature importance), and was selected as the primary model powering the dashboard's forecasts.

---

## 📊 Interactive Dashboard

A **Streamlit dashboard** was built to make the forecasting outputs accessible to non-technical stakeholders. It includes:

- **📈 Historical Sales** — explore past sales trends per store
- **🔮 Demand Forecast** — view N-day-ahead sales forecasts with confidence bands
- **🏷️ Promotion Impact** — compare sales distributions with and without promotions
- **📦 Inventory Recommendations** — translate forecasted demand into suggested stock levels

Users can select a store, adjust the forecast horizon, and instantly view updated charts, KPIs, and recommendations — no code required.

---

## 🧰 Tech Stack

- **Language:** Python
- **Data Processing:** Pandas, NumPy
- **Visualization:** Matplotlib
- **Machine Learning:** Scikit-learn, XGBoost
- **Deep Learning:** TensorFlow/Keras (LSTM demo)
- **Dashboard:** Streamlit
- **Development:** Jupyter Notebook (organized by pipeline phase)

---

## 📁 Project Structure

```
Retail-Demand-Forecasting/
│
├── notebooks/                # Phase-wise Jupyter notebooks (EDA, feature engineering, modeling)
├── app.py                    # Streamlit dashboard application
├── requirements.txt          # Project dependencies
├── models/                   # Saved trained model artifacts
├── data/                     # Raw and processed datasets (train/test/store)
└── README.md
```

---

## ⚙️ How to Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/mohamedfarithtechie/<repo-name>.git
cd <repo-name>

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the dashboard
streamlit run app.py
```

---

## 📈 Key Insights

- Promotions significantly increase average daily sales and customer footfall across most store types
- Sales exhibit strong weekly seasonality, with notable dips around state/school holidays
- Store type and assortment level are strong predictors of baseline sales volume
- XGBoost outperformed linear and ensemble baselines on RMSPE, making it the most reliable model for production-style forecasting

---

## 🔮 Future Improvements

- Incorporate external factors (weather, local events, economic indicators)
- Hyperparameter tuning via Bayesian optimization
- Deploy the model as a REST API for integration with inventory systems
- Extend the LSTM approach into a fully tuned deep learning forecasting model
- Add automated model retraining pipeline

---

## 👤 Author

**Mohamed Farith**
B.Tech, Artificial Intelligence & Data Science
[GitHub](https://github.com/mohamedfarithtechie) • [LinkedIn](https://linkedin.com/in/farithid)

---

## 📄 License

This project is open-source and available for educational and portfolio purposes.
