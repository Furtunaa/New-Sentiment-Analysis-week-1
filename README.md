# 📈 Predicting Price Moves with News Sentiment

### Nova Financial Solutions | Data Analytics Pipeline

[![CI/CD](https://github.com/YOUR_USERNAME/news-sentiment-analysis/actions/workflows/unittests.yml/badge.svg)](https://github.com/YOUR_USERNAME/news-sentiment-analysis/actions)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

🎯 Project Goal

Financial markets generate an enormous volume of news every day. While some headlines influence stock prices significantly, many have little or no impact. This project develops a complete analytical workflow designed to:

Analyze sentiment in financial headlines using NLP techniques with VADER
Generate technical indicators from historical stock market data using TA-Lib
Evaluate correlations between sentiment scores and stock returns through Pearson correlation analysis

## The pipeline aims to provide data-driven insights and support smarter investment decisions for Nova Financial Solutions.

## 📁 Project Structure

```
news-sentiment-analysis/
├── .github/
│   └── workflows/
│       └── unittests.yml       # CI/CD: pytest on push/PR
├── .vscode/
│   └── settings.json
├── .gitignore
├── requirements.txt
├── README.md
├── data/
│   └── raw/                    # FNSPID CSV + yfinance downloads
├── notebooks/
│   ├── task1_eda.ipynb          # Task 1: EDA
│   ├── task2_technical_indicators.ipynb  # Task 2: TA-Lib + PyNance
│   └── task3_correlation_analysis.ipynb # Task 3: Sentiment + Correlation
├── src/
│   ├── __init__.py
│   ├── eda_utils.py             # EDAAnalyzer class
│   ├── technical_indicators.py  # TechnicalAnalyzer class
│   ├── sentiment_analysis.py    # SentimentAnalyzer class
│   └── correlation_analysis.py  # CorrelationAnalyzer class
├── scripts/
│   ├── __init__.py
│   └── data_loader.py           # yfinance downloader + CSV loader
└── tests/
    ├── __init__.py
    └── test_pipeline.py         # pytest unit tests
```

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/news-sentiment-analysis.git
cd news-sentiment-analysis
```

### 2. Create virtual environment

```bash
python -m venv venv
source venv/bin/activate        # Linux/macOS
# venv\Scripts\activate         # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

> **TA-Lib Note:** On Linux, install system dependency first:
>
> ```bash
> sudo apt-get install libta-lib-dev   # Ubuntu/Debian
> brew install ta-lib                   # macOS
> ```
>
> On Windows, download the pre-built wheel from:
> https://github.com/cgohlke/talib-build/releases

### 4. Download NLTK data

```bash
python -c "import nltk; nltk.download('vader_lexicon')"
```

### 5. Download stock price data

```bash
python scripts/data_loader.py
```

### 6. Launch Jupyter

```bash
jupyter notebook notebooks/
```

---

📊 Project Tasks
Task 1 — Exploratory Data Analysis

Notebook: task1_eda.ipynb

Main analyses include:

Distribution of headline lengths
Publisher and email-domain analysis
News publication trends over time
TF-IDF keyword extraction
Heatmaps showing publication frequency patterns

**Key Visualizations:**
| Figure | Description |
|--------|-------------|
| Fig 1 | Headline length distribution + box plot |
| Fig 2 | Top 15 publishers by article count |
| Fig 3 | News volume over time with spikes |
| Fig 4 | Hourly publication pattern |
| Fig 5 | Day-of-week × hour heatmap |
| Fig 6 | Top 20 TF-IDF keywords |

---

### Task 2 — Technical Indicators (`task-2` branch)

**Notebook:** `notebooks/task2_technical_indicators.ipynb`

**TA-Lib Indicators:**
| Indicator | Parameters | Purpose |
|-----------|------------|---------|
| SMA | 20, 50 days | Trend direction |
| EMA | 20, 50 days | Responsive trend following |
| RSI | 14 days | Overbought/oversold signals |
| MACD | 12/26/9 | Momentum shifts |
| Bollinger Bands | 20, 2σ | Volatility envelope |
| ATR | 14 days | Volatility measure |

**PyNance-equivalent Metrics:**

- Sharpe Ratio (annualised)
- Sortino Ratio
- Maximum Drawdown
- Calmar Ratio
- Annualised Volatility

---

### Task 3 — Correlation Analysis (`task-3` branch)

**Notebook:** `notebooks/task3_correlation_analysis.ipynb`

- VADER sentiment scoring for all headlines
- Date alignment: weekends/holidays → next trading day
- Daily return calculation from Adj Close
- Pearson correlation coefficient per ticker
- Scatter plot (sentiment vs returns)
- Bar chart (average return by sentiment category)
- Rolling 30-day correlation over time

---

## 🧪 Running Tests

```bash
pytest tests/ -v --cov=src
```

Test coverage includes:

- EDA preprocessing and edge cases (null/empty headlines)
- VADER sentiment score range validation
- Technical indicator column presence and RSI bounds
- Pearson correlation result structure
- Date alignment (no weekend trade_dates)

---

## 🌿 Git Branch Strategy

```
main
├── task-1   (EDA)
├── task-2   (Technical Indicators)
└── task-3   (Sentiment & Correlation)
```

**Conventional Commits format:**

```
feat(eda): add TF-IDF topic modeling and publisher analysis
feat(indicators): compute SMA, EMA, RSI, MACD with TA-Lib
feat(correlation): add VADER sentiment scoring and Pearson correlation
fix(alignment): handle timezone-aware date parsing edge case
docs(readme): add installation instructions for TA-Lib on Windows
test(eda): add unit tests for headline length and publisher extraction
```

---

## 📚 Data Sources

| Dataset    | Source                                             | Description                                              |
| ---------- | -------------------------------------------------- | -------------------------------------------------------- |
| FNSPID     | Provided                                           | Financial news with headline, publisher, date, stock     |
| Price Data | [yfinance](https://github.com/ranaroussi/yfinance) | Daily OHLCV for AAPL, AMZN, GOOG, META, MSFT, NVDA, TSLA |

---

## 🔧 Key Dependencies

| Library        | Version | Purpose               |
| -------------- | ------- | --------------------- |
| pandas         | 2.2.2   | Data manipulation     |
| numpy          | 1.26.4  | Numerical computing   |
| matplotlib     | 3.9.0   | Visualizations        |
| seaborn        | 0.13.2  | Statistical plots     |
| yfinance       | 0.2.40  | Stock data download   |
| TA-Lib         | 0.4.28  | Technical indicators  |
| vaderSentiment | 3.3.1   | NLP sentiment scoring |
| nltk           | 3.8.1   | NLP toolkit           |
| scikit-learn   | 1.5.0   | TF-IDF vectorizer     |
| scipy          | 1.13.1  | Pearson correlation   |

---

## 📝 Key Findings (Summary)

1. **News Volume:** Spikes in publication frequency align with earnings seasons and macro events
2. **Publisher Concentration:** A small number of publishers (Benzinga, Reuters) dominate coverage
3. **Sentiment Distribution:** Financial headlines skew slightly positive (~55% positive)
4. **Correlation:** Weak positive correlation (r ≈ 0.03–0.12) between sentiment and same-day returns
5. **Investment Implication:** Sentiment works best as a **secondary signal filter**, not a primary trading trigger

---

## 👥 Team

| Role             | Name     |
| ---------------- | -------- |
| Team Facilitator | Kerod    |
| Team Facilitator | Mahbubah |
| Team Facilitator | Feven    |

**Submission Deadlines:**

- Interim: Sunday, 10 May 2026 — 8:00 PM UTC
- Final: Tuesday, 12 May 2026 — 8:00 PM UTC

---

## 📄 License

This project is for educational purposes as part of the 10 Academy program.
