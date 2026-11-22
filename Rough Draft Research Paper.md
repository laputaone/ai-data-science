# TITLE

Author: William Zhong  
DOI: \[FIGURE OUT LATER\]

## **Abstract**

This paper presents a study focused on finding the chances of reversion after a stock price dip in Mega and Large Cap companies taken from the S\&P 500\. The objective is to find how long the dip will last, what sectors are the most volatile, and what the chances are of recovery. The research includes data acquisition, cleaning, feature engineering, exploratory data analysis, and empirical evaluation. Mega Cap companies are defined as having over 100 Billion in market cap value, while Large Cap are defined as having less than 100 Billion and greater than 10 Billion. The study highlights which sector is safest to invest in, as well as how long you should hold a stock depending on the company.

## **1\. Introduction**

Stock price dips are common in public markets, which makes predicting a stock's rebound challenging for everyday investors. Finding how company size and sector types affect recovery speeds can help cut investment risk. Using quantitative models lets us examine past drops and calculate the real probability of price recovery.

This study looks at stock drops across S\&P 500 Mega Cap and Large Cap firms using standard data science techniques. The main goal is to measure sector volatility, estimate dip durations, and figure out the overall chances of recovery based on company characteristics.

## **2\. Methods and Dataset**

### **2.1. Dataset Description**

The dataset used in this study is taken from Yahoo Finance, containing 492 tickers from the S\&P 500 (The remaining tickers not taken were due to market cap not qualifying for Large Cap). Example Measurements include:

* **t:** Date  
* **o:** Opening Price  
* **c:** Closing Price  
* **h:** Daily High  
* **l:** Daily Low  
* **v:** Volume Traded  
* **sector:** What sector the company operates in

### **2.2. Data Preparing and Processing**

The core script, dip\_reversion\_analysis.py, executes the full analytical workflow. It first imports parameter settings and system paths via environment variables or default values (line 26), then retrieves the list of company tickers from a CSV file (line 50). From there, the program processes daily OHLCV price histories to isolate stock dips for each company (line 151), combines these events with Yahoo financial metadata (line 705), and exports all generated figures, summary tables, full reports, CSV datasets, and JSON files (lines 298, 561, and 724).

Potential price bottoms are determined using peak-detection methods on inverted closing figures (line 176). A successful rebound occurs when the stock price climbs back to its preceding high (line 207\) inside a maximum timeframe of MAX\_REVERSION\_DAYS \= 252 (lines 20 and 215), tracking both total calendar days and market trading days throughout the event window (lines 144 and 145).

To prevent script errors, missing sector data is managed through a three-tiered fallback system: unassigned sectors default to Unknown during metadata retrieval (line 111), convert to Unknown for every stock if external metadata is omitted and the merge step is bypassed (line 712), and are assigned Unknown following the merge operation (line 719). Consequently, any unclassified stocks are categorized under Unknown in all sector breakdowns and visualizations.

### **2.3. Exploratory Data Analysis (EDA)**

Figure 1 shows the distribution of calendar-day reversion windows across market sectors for recovered dip events within the 252-day maximum window, pairing individual event points with box plots showing the median, interquartile range, and whiskers. Across most sectors, median recovery times sit well below 100 calendar days, while the distributions are right-skewed with upper values extending near the 252-day limit. Event counts also vary substantially by sector—such as denser distributions in Technology and Unknown compared to sparser groups like Basic Materials and Financial Services—highlighting differences in sample volume and metadata coverage that inform how sector volatility and holding horizons are interpreted.

Figure 2 compares the overall dip reversion rate between Mega-Cap and Large-Cap equities, displaying the percentage of detected dips that recovered alongside exact event counts (recovered / total). Mega-Cap companies achieved a reversion rate of approximately 75.6% (362 of 479 dips), slightly outpacing Large-Cap companies at roughly 70.8% (2,903 of 4,101 dips), while Large-Cap represents a substantially larger total number of dip events.  
Figure 3 compares the percentage of recovered dips across market sectors, categorized by Mega-Cap and Large-Cap tiers. Within sectors containing both categories, Mega-Cap firms demonstrated superior recovery rates in Technology and Communication Services relative to Large-Cap peers, whereas Consumer Cyclical displayed a marginal advantage for Large-Cap equities. Multiple industries—such as Basic Materials, Industrials, Consumer Defensive, Utilities, Healthcare, Financial Services, and Energy—present data solely for Large-Cap companies, spanning from above 90% recovery in Basic Materials to approximately 57% in Energy.

Finally, Figure 4 examines individual company reversion rates across market capitalization on a logarithmic scale, overlaid with a 20-point moving average. Companies below the \$100 billion boundary exhibit wider dispersion in reversion likelihood—ranging from below 30% to over 90%—with the moving average sitting near 65%–70%. Above \$100 billion to \$200 billion, the moving average rises to roughly 73%–76% and remains stable across larger Mega-Cap equities, indicating that larger market capitalization is associated with more consistent recovery behavior rather than extreme downside outliers. 

Figure 5 compares calendar-day reversion windows between Mega-Cap and Large-Cap equities for recovered dips. Both tiers share nearly identical median recovery times of roughly 33 to 36 calendar days and lower quartiles near 13 days, though Mega-Cap exhibits a slightly narrower interquartile range (upper quartile near 91 days versus 98 days for Large-Cap) and a lower upper whisker. Both distributions remain heavily right-skewed toward the 252-day cutoff, showing that while typical recoveries occur within roughly one to three months, a substantial tail of dips requires extended holding windows regardless of market-cap tier. 

## 3\. Results and Discussions

Across the analyzed S\&P 500 sample, Mega-Cap equities demonstrated a higher overall dip reversion rate (\~75.6%, 362 of 479 events) than Large-Cap equities (\~70.8%, 2,903 of 4,101 events), with continuous market-cap trends showing recovery consistency stabilizing above the \$100 billion to \$200 billion threshold. Despite this gap in recovery likelihood, typical recovery timelines were consistent across both tiers, with median reversion windows near 33 to 36 calendar days and heavily right-skewed tails extending toward the 252-day cutoff. At the sector level, Mega-Cap equities outperformed Large-Cap peers in Technology and Communication Services, whereas lower-count sectors such as Basic Materials and Financial Services require cautious interpretation due to smaller sample sizes.

Several sources of potential error and bias shape these results. First, evaluating historical price series from current S\&P 500 constituents introduces survivorship bias, as companies that were delisted, acquired, or removed from the index after severe declines are excluded—likely inflating observed recovery rates relative to the broader historical market. Second, recovery is defined using a fixed 252-day maximum window (MAX\_REVERSION\_DAYS \= 252\) rather than a formal right-censored survival model, meaning dips requiring more than a year to rebound are classified as unrecovered within the study horizon. Finally, missing Yahoo sector data is retained under Unknown rather than discarded, preserving overall sample volume while separating unmapped equities in sector-level comparisons.

## 4\. Conclusion

The results demonstrate that historical price data and company metadata can effectively characterize dip reversion behavior across S\&P 500 equities. Mega-Cap companies exhibit slightly higher overall reversion rates and greater consistency above the \$100 billion threshold, while typical recovery timelines remain broadly similar across market-cap tiers and highlight how sector composition shapes downside variability.

The study underscores the importance of accounting for right-tail recovery risk, sector sample sizes, and survivorship bias rather than relying solely on headline rebound averages when setting holding horizons. Future research may focus on incorporating point-in-time historical index constituents to mitigate survivorship bias, applying formal survival analysis beyond the fixed 252-day window, or integrating additional macroeconomic and fundamental indicators for deeper cross-sector analysis.

## 

## References

Yahoo Finance. (2026). *Historical stock prices and company sector data* \[Data set\]. Yahoo. [https\://finance.yahoo.com/](https://finance.yahoo.com/)

Financial Industry Regulatory Authority. (2022, September 30). Market cap explained. FINRA. \[[https\://www\.finra.org/investors/insights/market-cap](https://www.finra.org/investors/insights/market-cap)\](https\://www\.finra.org/investors/insights/market-cap)  
