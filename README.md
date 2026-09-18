# Does the Stock Market Overreact? — Replication & Extension

## What is this project?

This is a master's-level replication of De Bondt and Thaler (1985), Does the Stock Market Overreact?

The paper studies whether stocks that performed poorly in the past tend to perform better later, while past winners tend to perform worse later.

I reproduce the main result with public data and then add one small extension.

## Research Question

> Can the main long-term reversal result from De Bondt and Thaler (1985) be reproduced with a modern public dataset?

The extension asks whether the reversal result is different in earlier and later parts of the available sample.

## Data

The original paper used CRSP data, which are not freely available.

For this project I use current S&P 500 constituents, monthly adjusted prices from Yahoo Finance, and an equal-weighted market return calculated from the sample.

This is not the same dataset as the original paper, and the difference is discussed in the notebooks.

## Notebook 1 — Replication

Notebook 1 explains the paper, prepares the data, forms winner and loser portfolios, calculates cumulative abnormal returns, and compares the result with the original paper.

## Notebook 2 — Extension

Notebook 2 splits the available formation dates into an earlier and later group and repeats the same calculation.

The purpose is to see whether the reversal result looks different across the sample period.

## Main Result

The public-data replication produces a reversal pattern, but the result is not identical to the original paper.

This is expected because the sample, stock universe, market measure, and data period are different.

The extension is exploratory and is not a full test of the later anomaly literature.

## Repository

01_replication.ipynb — replication
02_extension.ipynb — extension
data/ — data created by the notebooks
requirements.txt — required packages

## How to Run

pip install -r requirements.txt
jupyter notebook

Run 01_replication.ipynb first and then 02_extension.ipynb.

## Limitations

The biggest limitation is that I cannot use the original CRSP dataset.

Using current S&P 500 constituents creates survivorship bias, and the public sample is shorter and more recent than the original paper's sample.

The project is therefore a replication exercise rather than an exact reproduction.