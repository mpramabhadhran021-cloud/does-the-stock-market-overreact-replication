# Does the Stock Market Overreact? — Replication

A simple replication of De Bondt and Thaler (1985), *Does the Stock Market Overreact?*

## Question

Do stocks that performed badly in the past later perform better than stocks that performed well?

The original paper found evidence of long-term reversal. I try to reproduce the main idea using public data.

## Data

The original paper used CRSP data. I do not have access to CRSP, so I use:

- current S&P 500 constituents
- monthly adjusted prices from Yahoo Finance
- an equal-weighted market return calculated from the sample

Because I use today's S&P 500 members, the data have **survivorship bias**. So this is not an exact reproduction of the original paper.

## Method

I follow the main 3-year formation / 3-year test design:

1. Calculate monthly stock returns.
2. Calculate the equal-weighted market return.
3. Subtract the market return from each stock return.
4. Rank stocks using their previous 3-year performance.
5. Form winner and loser portfolios.
6. Track the portfolios for the next 3 years.
7. Compare the loser and winner returns.

## Files

- `01_replication.ipynb` — main replication
- `02_extension.ipynb` — simple time-split extension
- `data/` — data and results created by the notebooks
- `requirements.txt` — Python packages

## Extension

The second notebook splits the available formation periods into an early and a late group and repeats the same calculation.

This is only a small exploratory extension. It is not a full test of whether the anomaly disappeared after the original paper.

## Main limitation

The biggest limitation is the data. Current S&P 500 members are not the same as the historical stock universe used by De Bondt and Thaler.

So the goal of this project is **to understand and reproduce the method**, not to claim an exact reproduction of the original result.

## How to run

```bash
pip install -r requirements.txt
jupyter notebook
```

Run `01_replication.ipynb` first and then `02_extension.ipynb`.
