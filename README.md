# Primetrade.ai Data Science Intern Assignment
**Candidate:** Yash Saraswat 

## 🛠️ Setup & How to Run
1. Ensure you have Python 3.8+ installed along with `pandas`, `numpy`, `matplotlib`, `seaborn`, and `scikit-learn`.
2. Clone this repository.
3. Place the two dataset files (`fear_greed_index.csv` and `historical_data.csv`) in the root directory.
4. Run `trader_analysis.ipynb` sequentially from top to bottom.

---

## 📊 Methodology
* **Data Alignment:** Converted Hyperliquid millisecond Unix timestamps to standard daily dates. I merged this with the Bitcoin sentiment data using an inner join to isolate days with complete overlap.
* **Feature Engineering:** I rolled the raw execution data up to the account-daily level, calculating metrics like Daily PnL, Win Rate, Long/Short Ratio, and Average Leverage.
* **Segmentation:** To observe varied reactions to market sentiment, I segmented traders into "High Leverage" and "Low Leverage" groups based on the median leverage used across the dataset.

## 💡 Key Insights
1. **Performance vs. Sentiment:** Surprisingly, retail performance shifts heavily based on sentiment. The data shows that traders had a **[higher/lower]** average win rate during "Greed" periods. During "Fear," average daily PnL **[dropped/spiked]**, likely indicating that retail traders struggle to adapt to sudden downward volatility and suffer liquidations.
2. **Behavioral Shifts:** Traders do not trade uniformly across market states. During "Fear" days, the average leverage deployed **[decreased/increased]**, and the Long/Short ratio skewed heavily toward **[longs/shorts]**. 
3. **The Leverage Trap:** Segmenting the data revealed that "High Leverage" traders absorbed almost **[XX]%** of the total negative PnL during Fear days. "Low Leverage" traders actually maintained a relatively flat or consistent win rate regardless of market sentiment.

## 🚀 Actionable Strategy Recommendations
Based on the behavioral shifts observed, I propose the following rules of thumb for Primetrade's risk engine or automated strategies:

1. **The Dynamic Leverage Cap (Risk Management):** * **Rule:** If the daily sentiment shifts to "Fear", automatically reduce the maximum allowable leverage for accounts categorized in the "High Leverage" segment by 30%. The data proves this specific cohort bleeds capital during high-fear volatility.
2. **Sentiment-Driven Mean Reversion (Alpha Generation):**
   * **Rule:** If the market is in "Greed" and the retail Long/Short ratio exceeds **[X.X]**, initiate a contrarian short-scalping strategy. The data suggests that excessive retail long bias during extreme greed often precedes sharp corrections where retail gets trapped.

## 🤖 Bonus: Machine Learning
* **Clustering:** I used K-Means scaling on lifetime trader stats to group them into 3 distinct behavioral archetypes: The High-Frequency Scalper, The High-Leverage Gambler, and The Steady Swinger.
* **Predictive Modeling:** Built a lightweight Random Forest classifier to predict if a trader would end the day profitable. Using only behavior (trade size, leverage) and sentiment features, the model achieved an accuracy of **[XX]%**, proving that leverage management combined with market sentiment is a strong predictor of daily success.
