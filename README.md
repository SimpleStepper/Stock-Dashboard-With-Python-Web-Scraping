# Stock Dashboard with Python Web Scraping

This is a project I built to make tracking stock market portfolios easier and more insightful using Python Web Scraping and Tableau. The idea was to automate data collection, merge it with personal holdings, and visualize everything clearly — all without relying on expensive tools or manual processes.

<img width="1073" height="714" alt="image" src="https://github.com/user-attachments/assets/01e16a96-1288-46d3-b4c9-c1070f9fe840" />

**🔗 Dashboard**

You can explore the final Interactive Tableau dashboard here: 

[Stock Portfolio Dashboard](https://public.tableau.com/app/profile/robert.smith7087/viz/StockPortfolioDashboard_17527175741930/StockPort2#1.)

I built this to solve a problem: 

Quickly see how stocks are doing, **in the context of the broader market**, without logging into multiple platforms.

🛠️ **How It Works**

1) **Web Scraping and Automation (Python)**
   - Reads a excel sheet with invested stock tickers
   - Uses Yahoo Finance API (yfinance) to pull historical and latest stock prices
   - Uses Pandas to clean, reshape and reintegrate the data into the same Excel Sheet
   - Handle cross validation and data alignment using XLOOKUP
  
2) **Dashboard (Tableau)**
   - **Portfolio Performance** - gain/loss per stock and allocation
   - **General Market Trends** - broad market movements for context and insights
   - Design for non-technical users to easily explore and generate (and answer) questions about their investments
  
---

**Technical Hightlights**

**Python** 

Full Code for this project with notes can be found here: [Stock Python Web Scraping](https://github.com/SimpleStepper/Stock-Dashboard-With-Python-Web-Scraping/blob/main/Stock%20Market%20Scraper.ipynb)

I wanted to highlight specifically the Web scraping element of the project, as it was a fantastic learning experience to combine my Pandas skillset with real world data. 

```python
#Create that seperates mutual fund data and stock data
mutual_funds = []
stocks_etfs = []

for symbol in tickers:
    if symbol.endswith("X"):  # most mutual fund tickers end in X
        mutual_funds.append(symbol)
    else:
        stocks_etfs.append(symbol)

#Yahoo finance API to recieve stock data
stock_data = yf.download(stocks_etfs, start="2000-01-01", auto_adjust=True)
mutual_funds_data = yf.download(mutual_funds, start="2000-01-01", auto_adjust=True)

historical_stock_df = pd.concat([stock_data["Close"], mutual_funds_data["Close"]]) # Combines Stocks and Mutual Funds into One dataframe (excel sheet)
historical_stock_df.reset_index=True # Resets indexing to start over with new columns 
historical_stock_df.fillna("", inplace=True) # fills Null values with Blanks instead of Errors/random data
historical_stock_df = historical_stock_df.sort_values(by='Date', ascending=False) # Sorts the data from Descending data (starts at 2025 rather than 2000)
```

This is the code that connects to Yahoo Finance and pulls it into a Pandas data frame to reinsert into our original excel. 

**Tableau** 

![Untitled video - Made with Clipchamp](https://github.com/user-attachments/assets/bcbe1eb4-2ad9-4915-b6d6-7e80807ccaa1)


*Custom Calculated Fields*
Built Tableau fields for:

- Percent gain/loss

- Total value over time

- Cumulative return

- Individual vs. portfolio trends

*Dynamic Interactivity*

- Implemented dashboard actions like ticker filtering, time zoom, and performance sorting, allowing users to interact with the data without needing to understand Tableau internals.

*Market Context Layer*

- Pulled in SPY index and other market indicators to visually correlate individual stock performance against broader trends.

*Responsive Dashboard Layout*

- Designed for public sharing (via Tableau Public), ensuring performance and readability on a variety of screen sizes and resolutions.



**Technical Skills Demonstrated:**

- Data Integration: Successfully combined personal portfolio data with real-time market data via Yahoo Finance API
- Data Processing: Used pandas for data manipulation, cleaning, and Excel integration
- Visualization: Created interactive Tableau dashboards with meaningful insights
- Automation: Built a scraper that automates data updates
