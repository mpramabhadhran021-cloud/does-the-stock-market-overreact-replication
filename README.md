# Does the Stock Market Overreact? — Replication & Extension

Master's-level research project replicating De Bondt, W. F. M. & Thaler, R. (1985), *"Does the
Stock Market Overreact?"*, **The Journal of Finance**, 40(3), 793–805, and extending it with one
small, literature-motivated follow-up analysis.

## Structure

```
README.md
requirements.txt
01_replication.ipynb   # reproduces the paper's main result with public data
02_extension.ipynb     # extension: has the reversal spread weakened over time?
data/                  # created/cached by the notebooks on first run
  sp500_constituents.csv   # ticker universe (included; re-downloaded automatically if missing)
  monthly_prices.csv       # price panel (built by Notebook 1; not included — see below)
  excess_returns.csv       # market-adjusted excess returns (built by Notebook 1)
  replication_car_results.csv  # per-replication CAR results (built by Notebook 1, used by Notebook 2)
```

Run **`01_replication.ipynb` first, top to bottom**, then `02_extension.ipynb`. Notebook 2 reads
`data/replication_car_results.csv`, which Notebook 1 produces.

## What each notebook contains

**Notebook 1 — Replication.** Paper summary, research question and hypotheses, data sourcing and
cleaning, a full implementation of the original 3-year formation / 3-year test, decile-portfolio,
market-adjusted-excess-return methodology (including the paper's own pooled-variance t-statistic),
the headline result, a side-by-side comparison with the original paper's numbers, and a discussion
of similarities/differences.

**Notebook 2 — Extension.** Motivated by the later "anomalies decay after publication" literature
(McLean & Pontiff, 2016), it splits the replication's formation dates into an early and a late
sub-sample and re-runs the *same* ACAR/t-statistic computation on each, to see whether the
reversal spread has weakened within the (already post-1985) window our data covers.

## Data

The original paper uses CRSP (NYSE common stocks, 1926–1982), a proprietary database we don't
have access to. We substitute a free, public alternative:

- **Universe:** current S&P 500 constituents (`data/sp500_constituents.csv`, from a public
  GitHub mirror of the Wikipedia constituents table).
- **Prices:** monthly adjusted close from Yahoo Finance, via the `yfinance` package, roughly
  1995–present.
- **Market index:** equal-weighted average return across the sample each month (a proxy for the
  CRSP equal-weighted index used in the original).

This is a disclosed, deliberate simplification made necessary by data access, not an attempt to
match CRSP exactly. It introduces survivorship bias and a shorter, more recent, lower-power sample
than the original — this is discussed explicitly in both notebooks.

**Reproducibility note.** `01_replication.ipynb` downloads price history via `yfinance`, which
needs a normal internet connection to Yahoo Finance. Once downloaded, prices are cached to
`data/monthly_prices.csv` so later cells, re-runs, and Notebook 2 never need to re-download
anything. (This repository ships `data/sp500_constituents.csv`, a small ticker list fetched from a
GitHub mirror, but not the larger price panel, which each user should download fresh.)

## Environment

```
pip install -r requirements.txt
jupyter notebook
```

## Scope and honesty about limitations

This project deliberately replicates only the paper's headline 3-year/3-year result and pursues
one manageable extension, rather than every robustness table in the original (1-, 2-, and 5-year
formation variants, CAPM-beta comparison, January-seasonality tables). Every methodological choice
and every deviation from the original paper is called out explicitly in the notebooks, and both
notebooks interpret their own numbers programmatically (via `f-string`-driven narrative cells) so
the written discussion always matches whatever the code actually produces when run — nothing here
is a fabricated or hard-coded result.
