# Bitcoin Historical Data Analysis with TA-Lib

This repository contains a Python script to analyze Bitcoin historical data using various technical indicators and candlestick patterns. The analysis identifies trends and patterns that can be used for trading or research purposes.

## Table of Contents

- [Introduction](#introduction)
- [Dataset](#dataset)
- [Google Colab Setup](#google-colab-setup)
- [Code Overview](#code-overview)
- [Features Explained](#features-explained)
- [Running the Code](#running-the-code)
- [Results](#results)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This project focuses on analyzing Bitcoin historical data, leveraging technical indicators like Simple Moving Averages (SMA), Average True Range (ATR), and various candlestick patterns provided by the TA-Lib library. The goal is to identify trends, calculate performance periods, and extract meaningful insights from the data.

## Dataset

The dataset used for this analysis is the [Bitcoin Historical Data](https://www.kaggle.com/datasets/mczielinski/bitcoin-historical-data) available on Kaggle. It includes minute-level data from 2012 to 2021.

## Google Colab Setup

To run this code on Google Colab, follow these steps to upload your Kaggle API key and install the necessary packages:

```python
from google.colab import files
files.upload()  # Upload your kaggle.json file
!mkdir -p ~/.kaggle
!cp kaggle.json ~/.kaggle/
!chmod 600 ~/.kaggle/kaggle.json
!pip install kaggle
!kaggle datasets download -d mczielinski/bitcoin-historical-data
!unzip bitcoin-historical-data.zip
!curl -L http://prdownloads.sourceforge.net/ta-lib/ta-lib-0.4.0-src.tar.gz -O && tar xzvf ta-lib-0.4.0-src.tar.gz
!cd ta-lib && ./configure --prefix=/usr && make && make install && cd - && pip install ta-lib
```

These commands will:
1. Upload your Kaggle API key to access the dataset.
2. Download the Bitcoin historical data.
3. Install TA-Lib, a library for technical analysis.

## Code Overview

The main script performs the following tasks:

1. **Data Loading and Preparation**: 
   - Loads the Bitcoin historical data from a CSV file.
   - Resamples the data to an hourly timeframe for analysis.

2. **Indicator Calculation**:
   - Calculates various technical indicators including SMA, ATR, and others.
   - Resamples the data to a daily timeframe to calculate daily trends.

3. **Trend Identification**:
   - Identifies uptrends, downtrends, and sideways trends using SMA50 and SMA200.

4. **Candlestick Pattern Analysis**:
   - Analyzes all candlestick patterns provided by TA-Lib.
   - Evaluates the performance of these patterns in predicting bullish and bearish movements.

5. **Detailed Analysis**:
   - Summarizes the results for each candlestick pattern in terms of occurrences, trend alignment, volume conditions, and more.

## Features Explained

The script calculates and uses several features to conduct the analysis:

- **SMA50 & SMA200**: These are the 50-period and 200-period Simple Moving Averages of the closing price, respectively. They help in identifying trends, where:
  - SMA50 > SMA200 indicates an **Uptrend** (often referred to as a "Golden Cross").
  - SMA50 < SMA200 indicates a **Downtrend** (often referred to as a "Death Cross").

- **ATR (Average True Range)**: A volatility indicator that measures the degree of price movement for a given time period. It is used to assess the volatility of the market.

- **Volume_MA_20**: A 20-period moving average of the trading volume. It helps in identifying periods of high or low volume relative to the recent past.

- **Candle_Size**: The difference between the high and low prices for each hour. This feature is used to assess the size of the candlestick.

- **Next_Close_Change**: The percentage change in the closing price of the next time period. This helps in predicting the direction of the market.

- **Prev_High & Prev_Low**: These represent the previous period's high and low prices, used to identify support and resistance levels.

- **Daily_Trend**: The trend calculated from the daily resampled data, specifically the 20-period SMA of daily closing prices. It provides a broader context to the hourly data.

- **Trend**: This feature identifies whether the market is in an uptrend, downtrend, or moving sideways. The sideways trend is defined as when the closing price is within 2% of the SMA50.

- **Volume_Condition**: This binary feature indicates whether the trading volume is above or below the 20-period volume moving average.

- **Candle_Size_Relative**: The size of the candlestick relative to the ATR, indicating whether the candlestick is large or small compared to recent volatility.

- **Support_Resistance**: This feature identifies whether the closing price breaches the previous high or low, indicating a potential breakout or breakdown.

- **Daily_Trend_Alignment**: This checks if the closing price is above or below the daily trend SMA, indicating whether the short-term price action aligns with the longer-term trend.

## Running the Code

After setting up the environment in Google Colab or your local machine, you can run the provided script to perform the analysis.

```python
# Simply run the script after setting up your environment.
```

## Results

The script generates a detailed analysis of various candlestick patterns, which is stored in a DataFrame and can be saved as a CSV file (`kaggle_hourly_pattern_analysis.csv`). The analysis includes statistics such as average close change, trend alignment, and volume conditions for each pattern.

## Contributing

Contributions are welcome! If you have any improvements or new features to add, feel free to open a pull request or issue.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
