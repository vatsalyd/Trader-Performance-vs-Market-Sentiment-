# Trader Performance vs Market Sentiment — Primetrade.ai Round 0

Analysis of how Bitcoin market sentiment (Fear/Greed) relates to trader behavior and profitability on Hyperliquid.

---

## Datasets

| File | Description |
|---|---|
| `fear_greed_index.csv` | Daily Bitcoin Fear & Greed Index (value 0–100 + classification) |
| `historical_data.csv` | ~211K Hyperliquid trade records across 32 accounts (2023–2025) |

---

## Setup

```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy nbformat
```

Then place both CSV files in the same directory as the notebook and run all cells top-to-bottom.

---

## Notebook Structure

**Part A — Data Preparation**
- Shape, missing values, and duplicate checks on both datasets
- Timestamp parsing and daily alignment via inner join on date
- Feature engineering: daily PnL, win rate, trade frequency, long ratio, position size per trader

**Part B — Analysis**
- Performance (PnL, win rate) on Fear vs Greed vs Neutral days with t-test
- Behavioral shifts in trade frequency, position size, and long/short bias across sentiment regimes
- Three trader segments: position size, trade frequency, and PnL consistency
- Four charts covering all key comparisons

**Part C — Strategy Recommendations**
- Two actionable rules derived directly from the data

**Bonus**
- Random Forest classifier predicting next-day profitability (67% accuracy vs 57% baseline)
- K-Means clustering into three behavioral archetypes

---

## Key Findings

1. **Fear days are more profitable.** Average daily PnL is ~25% higher on Fear days ($5,185) than Greed days ($4,144), despite win rates being nearly identical. Larger winning trades — not more of them — drive the gap.

2. **Traders behave counter-cyclically.** During Fear periods, traders increase position sizes (+43% vs Greed days) and trade more frequently (+37%), suggesting systematic "buy the dip" behavior rather than panic.

3. **Consistency amplifies the Fear-day edge.** Consistent winners earn 2.4× more on Fear days than Greed days. Inconsistent traders show no such pattern — making sentiment-responsive sizing a skill-dependent strategy, not a general rule.

---

## Strategy Recommendations

**Fear-Day Protocol**
When the Fear/Greed index drops below 40, consistent traders should increase position sizes by 20–30% and bias toward long entries. This formalizes a behavior the data shows is already profitable for this segment.

**Greed-Day Discipline**
When the index exceeds 60, frequent traders should reduce trade count by ~25% and focus on closing existing positions rather than opening new ones. Per-trade edge compresses during Greed periods; preserving capital for Fear windows is the better play.

---

## Repository Structure

```
├── assignment.ipynb   # Main notebook (fully executed)
├── fear_greed_index.csv        # Sentiment dataset
├── historical_data.csv         # Trader dataset
└── README.md
```
