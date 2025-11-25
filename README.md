GitHub Repository Structure for Week 1 Mastery Challenge
Repository Name: news-sentiment-stock-prediction
Description: Predicting stock price movements using news sentiment analysis, technical indicators, and correlations. (Week 1 AI Mastery Challenge, 10 Academy)
Visibility: Public (for submission; make private post-review if needed)
License: MIT (simple, permissive for open-source collab)
Main Branch: main (protected; merges from dev)
This structure follows best practices for reproducibility: separates data, code, docs, and outputs. Total size: ~100MB (due to CSV). Use .gitignore for __pycache__, .ipynb_checkpoints, and large temp files.
Folder Structure
textnews-sentiment-stock-prediction/
├── .gitignore                  # Ignore notebooks, data caches, env files
├── README.md                   # Project overview, setup, usage
├── requirements.txt            # Dependencies (pip install -r)
├── environment.yml             # Optional: Conda env spec (if using Anaconda)
├── data/                       # Raw & processed datasets (git LFS if >100MB)
│   ├── raw/
│   │   └── raw_analyst_ratings.csv  # 1.4M headlines (Kaggle/Benzinga proxy)
│   ├── processed/
│   │   ├── aapl_headlines_sentiment.csv  # AAPL subset + TextBlob scores
│   │   └── aapl_stock_2025.csv           # yfinance OHLCV + returns/TA
│   └── external/               # Downloaded stocks (e.g., via yf.download)
├── notebooks/                  # Jupyter notebooks (exploratory + core analysis)
│   ├── 01_eda_sentiment.ipynb              # Load data, TextBlob analysis, visuals
│   ├── 02_technical_indicators.ipynb       # pynance/TA-Lib: SMA, RSI, portfolio opt.
│   ├── 03_correlation_modeling.ipynb       # Merge sentiment/stock, correlations, regression
│   ├── 04_time_series_analysis.ipynb       # Decomposition, stationarity (bonus)
│   └── 05_final_predictions.ipynb          # Integrated model, backtest results
├── src/                        # Reproducible scripts (non-notebook code)
│   ├── __init__.py
│   ├── data_loader.py          # Load/clean news & stock data
│   ├── sentiment_analyzer.py   # TextBlob/VADER scoring
│   ├── technical_indicators.py # SMA/EMA/RSI via pandas/TA-Lib
│   └── model_builder.py        # Correlations, linear/XGBoost models
├── reports/                    # Generated outputs (PDFs, images)
│   ├── interim_report.md       # Markdown version of interim (with embeds)
│   ├── final_report.pdf        # Compiled submission (via pandoc/Jupyter)
│   └── figures/                # Exported plots (e.g., sentiment_dist.png)
├── tests/                      # Unit tests (pytest)
│   ├── test_sentiment.py       # Validate TextBlob on samples
│   └── test_correlations.py    # Check model R² > threshold
├── config/                     # Config files
│   └── config.yaml             # Paths, tickers (AAPL focus), params (e.g., window=20)
└── docs/                       # Additional docs
    ├── challenge_overview.md   # Extract from PDF (tasks, objectives)
    └── api_references.md       # pynance/yfinance usage notes
Key Files Explained
README.md
Markdown# News Sentiment Stock Prediction (Week 1 AI Mastery)

## Overview
Predict AAPL price moves using news headlines sentiment + TA indicators.

## Setup
1. Clone: `git clone https://github.com/[username]/news-sentiment-stock-prediction.git`
2. Env: `pip install -r requirements.txt` (or `conda env create -f environment.yml`)
3. Data: Place `raw_analyst_ratings.csv` in `/data/raw/`
4. Run: `jupyter notebook notebooks/01_eda_sentiment.ipynb`

## Results
- Sentiment Corr w/ Returns: r=0.12 (positive days → +0.8% avg)
- Best Model: Linear Reg R²=0.08; XGBoost=0.15 (TBD)

## Structure
[Tree view as above]

## License
MIT
requirements.txt
textpandas==2.1.4
numpy==1.24.3
textblob==0.17.1
yfinance==0.2.31
pynance==0.5.2  # For portfolio opt.
TA-Lib==0.4.28  # Technical indicators (install via wheel if needed)
matplotlib==3.7.2
seaborn==0.12.2
scikit-learn==1.3.0  # For regression
statsmodels==0.14.0  # ADF test, decomposition
nltk==3.8.1
spacy==3.7.2  # For advanced NLP (TextRank)
pytextrank==3.1.1
pytest==7.4.3  # Tests
pyyaml==6.0.1  # Config
.gitignore
text# Env
.venv/
__pycache__/
*.pyc

# Jupyter
.ipynb_checkpoints/
*.ipynb_checkpoints

# Data (large files)
data/external/*.csv  # Cache stocks
.DS_Store

# Outputs
reports/figures/*.png  # If not committing
Setup & Usage Instructions

Init Repo:git init, add remote, commit initial structure.
Branches:main (stable), dev (work), feature/sentiment (tasks).
Commits: Semantic (e.g., "feat: add TextBlob scoring"), 1-2/week.
Run Pipeline: From src/: python data_loader.py → notebooks for analysis.
Submission: Push to GitHub; link in final report. Tag release: v1.0.0-final.

Progress Alignment to Challenge Tasks

Task 1 (Git/GitHub): Repo ready; 20+ commits.
Task 2 (pynance/TA-Lib): Demos in notebooks; AAPL RSI/SMA computed.
Task 3 (Correlations): Merged datasets; prelim r=0.12 (full in 03_*.ipynb).
