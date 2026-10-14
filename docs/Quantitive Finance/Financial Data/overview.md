[TOC]

# Best Practice

## Table of Contents
* [The Evolution and Importance of Data in Finance](#the-evolution-and-importance-of-data-in-finance)
    * [Table: Tools](#tools)
* [Types of Financial Data](#types-of-financial-data)
* [Table: Data Sources](#data-sources)
* [Table: Data Descriptors and Identifiers](#data-descriptors-and-identifiers)
    * [Table:  Fungible Asset VS Infungible Asset](#fungible-asset-vs-infungible-asset) 

## The Evolution and Importance of Data in Finance
Financial data has evolved from traditional market data & corporate financial statements to increasingly valuable real-time **alternative datasets** (e.g., health, satellite images, climate, pullution, education, etc.), because economics is intertwined with society and any data produced can be seen from an economic perspective. 

### Tools
| Category  | Tools | Use Case |
|-------|---------|-------------|
|cloud infrastructure | <br> • Apache Kafka <br> •  Amazon Kinesis <br> • Google Cloud Pub/Sub <br> •  Microsoft Azure Event Hubs |stream and process millions of events per second.|
|programming| <br> • Python (NumPy, Pandas, SciPy) <br> • R <br> • Jupyter Notebooks| data analysis, manipulation, visualization |
|terminals| <br> • Bloomberg Terminal <br> • Thomson Reuters Eikon |  real-time analytics and financial data for trading and risk management.|
|numerical environments| MATLAB & Mathematica| research|
|statistical software|<br> • SAS <br> • Stata <br> • EViews|data analysis, econometric modeling, and forecasting|
|protocols| <br> • WebSocket Protocol <br> • Financial Information Exchange (FIX) <br> •  Protocol Precision Time Protocol (PTP) | <br> • WebSocket: continuous, bidirectional, and persistent connection between the client and the server <br> • FIX: vendor-agnostic messaging standard between financial institutions. <br> •  PTP: time synchronization across networks to ensure that trades are accurately time-stamped to the microsecond.|
-------


## Types of Financial Data

| **Data Type** | **Definition & Structure** | **Examples** | **How to Store in Python** | **Notes** |
|----------------|-----------------------------|---------------------------|-----------------------------------------------|-------------------------|
| **Structured Data** | tabular or matrix with clearly defined rows and columns. <br> • Each column = variable <br> • each row = observation time (one busines day / intraday). | Stock prices matrix of all the stocks within an exchange-traded fund.<br>• Cross-section: each row  = portfolio snapshot <br>• Time series: each column  = stock history | • best choice: `pandas.DataFrame`  <br> • homogeneous numeric data and speed: `numpy.array` | Long-term storage depends on use case: <br>  •  storing and querying time-series data: **Time Series Databases (TSDB)** (InfluxDB, KDB+/q, TimescaleDB, Prometheus) <br>  • big data analytics: **Columnar files** (Apache Parquet, ORC) 👎 slow loading times <br>  • easy to read: **Human-readable** (CSV, Excel) 👎 not efficient.<br>  • large numerical datasets and complex data hierarchies: **HDF5** |
| **Unstructured Data** | non-numerical data without predefined schema or tabular organization <br> (e.g., text, social media post, review sites, images, audio, video.) | • social media posts, news, customer reviews/ Instagram photos for company stock <br>• Satellite images for weather derivatives | • Handled via `dict` and `list` because nested containers support mixed data types | <br> • use ML models to do sentiment analysis  <br> • Difficult to store |
| **Semi-Structured Data** | Between structured and unstructured; contains some schema (tags, fields) but allows flexibility in format and nesting. | • Emails (“To,” “From,” “Subject,” text body) <br>• JSON / XML files(schema could change from file to file and contains nested data structures.) | • `dict`,`list` for nested fields <br>• `pandas.DataFrame` with `MultiIndex` for tabular tags/schema | • More indexable and searchable than unstructured data |



## Data Sources

| **Category** | **Examples** | **Notes** |
|---------------|--------------|-----------|
| **Primary Sources** | <br> •  exchanges (stock, option, commodity, forex, cryptocurrency) <br> • credit agencies  | raw complete data  (quotes & trades). Highest accuracy |
| **Financial Platforms** | Bloomberg Terminal, Refinitiv Eikon, FactSet | redistributors of data from exchanges, OTC markets, and other financial sources. |
| **Data Vendors** | BarChart, RavenPack, Capital IQ, CRISP, Datastream, Morningstar, Exante Data,Xignite, Refinitiv, Short Trends, dxFeed | clean/raw data; via APIs  |
| **Free Public Sources** | Quandl, Alpha Vantage, FRED: Federal Reserve Economic Database, , Google Finance, Yahoo Finance | Public/educational access; limited ammount can be accessed |


### note
- **Quote = bid + ask prices**, showing willingness to trade.  
- **Trade = executed transaction** once bid = ask.  
- **OTC (Over-the-Counter)** markets are decentralized networks (e.g., bonds, derivatives) traded directly between parties, not on an exchange.


## Data Descriptors and Identifiers
allow you to link data precisely to specific securities.  
| **Identifier / Concept** | **Full Name & Meaning** | **Used For / Scope** | **Format & Structure** | **Key Notes** |
|---------------------------|--------------------------|----------------------|------------------------|----------------|
| **Ticker** | Short symbol used to identify publicly traded companies on exchanges. | Stocks, ETFs | Typically 1–5 letters (e.g., AAPL, IBM). |<br> • most popularly known identifiers;  <br> • often resembles company name or type.  <br> • not used for bonds. |
| **CUSIP** | *Committee on Uniform Security Identification Procedures* | North American securities (stocks, bonds, options). | 9-character alphanumeric code: <br>• First 6 = issuer <br>• Next 2 = security type <br>• Last 1 = check digit (created correctly) | <br> • Unique to U.S. & Canada. <br> • **CINS** (International Numbering System) is a CUSIP for securities in foreign markets (adds issuing country prefix). |
| **SEDOL** | *Stock Exchange Daily Official List* | UK and some global markets. | 7-character alphanumeric identifier. | <br> • Assigned when a company is listed on an exchange; removed when delisted. <br> •  Example: Hertz changed SEDOL after moving from NYSE → NASDAQ in 2020. |
| **ISIN** | *International Securities Identification Number* | Global standard for identifying securities across markets internationally. | 12-character code: <br>• First 2 = country <br>• Next 9 = security | <br> •  more universal <br> • e.g., futures tend not to have CUSIPs but do have ISINs. Foreign exchange rates have identifiable tickers (e.g., GBP/USD) but are referred to internationally by their ISINs. |



### Fungible Asset VS Infungible Asset
| **Concept** | **Meaning**  | **Indentification**| **Used For / Scope** |
|---------------------------|--------------------------|--------------------------|----------------------|
| **Fungible Asset** | Interchangeable asset with identical value but ≠ identical asset |  identifiers | Stocks, bonds, ETFs, gold, Bitcoin, paper currency in any country, <br> diamonds without engraved serial number by GIA (with risks that it is not properly appraised for clarity or carats or might be actually man-made or fake.) |
| **Infungible Asset** | Unique or non-interchangeable items. | no identifiers, use deed or property record, often filed at the local level | Real estate, art, jewelry (Diamonds with engraved serial number by GIA), collectibles. |


## Time Zones, Trading Days, and 24/7 Trading

Financial data across markets occur in **different time zones** and **trading hours**, so even simple comparisons (like daily prices or returns) can be misleading if timestamps are not aligned.  
Always verify *when* data was recorded before calculating correlations, returns, or building strategies.


| **Concept** | **Meaning** | **Example or Implication** |
|--------------|---------------------------|-----------------------------|
| **Asynchronous data** | A single day’s close price varies by geographic market and time zone.  | Lagos (GMT+1) vs. Sydney (GMT+10) = 9-hour difference between official closes.  →  adjust timestamps to a common reference (e.g., GMT).|
| **Timestamp alignment** | Before analyzing or correlating data, adjust local timestamps to a common reference (e.g., GMT). | Note: For statistical analysis, e.g., correlation, use both markets’ *latest available* data (e.g., close price). |
| avoid **reversing cause and effect** | Do not use information not yet known at the time of trading, which creates a false predictive signal. | If you were to build a trading strategy using closing price correlation and decided to buy XX, it would have to be for the following trading day. |
| **OTC market issue** | OTC (Over-The-Counter) instruments trade across cities without a central exchange. There is no single “official closing price” for the day and each trading center (Tokyo, London, New York) has its own “closing quote.”| The quality of your **data vendor** become critical. (Are they providing the time zone, market, currency, etc.?) |
| **24/7 trading assets** | Some assets (e.g., Bitcoin) trade continuously. there’s no daily closing. | data vendors pick an consistent daily cutoff time to define a “daily close.” (e.g., 00:00 GMT) for daily aggregation.  |


### 💡 Takeaways
- Always check **timestamp, time zone, and trading-day definitions** before comparing markets.  
- Even daily or closing-price data require **time alignment** to avoid misleading results.  
- **Don’t mix data from different local days** — otherwise, you may introduce **look-ahead bias**.  
- **OTC and crypto markets** complicate this further because they lack a universal close time.  
- Consistency is more important than local convention — pick one time reference (e.g., GMT) and apply it to all data.

