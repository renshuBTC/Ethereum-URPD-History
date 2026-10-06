# Ethereum URPD History: ETH realized price distribution, every day since 2015

**Website: [EthereumURPD.com](https://www.ethereumurpd.com/)**

The Ethereum URPD (realized price distribution) sorts all ETH by the price at which it last moved on-chain and adds up
the supply at each price. EthereumURPD.com draws it for every day since Ethereum's launch on 30 July 2015, each bar
split into short- and long-term holders (LTH/STH) or into 23 age bands. It is a cost-basis distribution of the whole
ETH supply: it shows at which prices the supply last moved, and how much of it is in profit or in loss at each day's
price.

## What the site shows

- **% USD or % ETH.** Each price bucket's share of the day: of the realized value (every coin's value when it last
  moved, added up) or of the ETH supply. A day's bars add up to 100%.
- **LTH/STH or AGE.** Short- and long-term holders at Ethereum's own boundary of 124 days, worked out from its history
  with Glassnode's method, with Glassnode's logistic weight 10 days wide (half long-term held at 124 days, 90% at 146);
  or 23 age bands, from under an hour to over 15 years.
- **Supply in profit and in loss** at the day's ETH price, and a bottom signal when at least 90% of the value
  (% USD) or 70% of the coins (% ETH) is in loss; both thresholds can be changed in the toolbar.
- **ETH's price** as a line of daily closes, with past cycle tops and bottoms marked.
- **An explainer** of how to read the chart, in English, Chinese and Japanese.
- **Four full-history videos** on YouTube, one for each weighting and colouring (% USD or % ETH, LTH/STH or AGE):
  5 minutes each, 4K at 60 frames a second. The video buttons in the toolbar open them.

## Scrubbing through history

- Drag the orange dot along the price line to any day.
- **← / →** or **A / D**: one step back or forward; **1D / 1W / 1M / 1Y** (keys **1** to **4**) set the step;
  **↑ / ↓** or **W / S** change it one size; **Home / End**: the first and the latest day.
- **CYCLE TOP/BTM** jumps to a cycle top or bottom.
- Click and drag across the chart to mark a price range: it gives the share of the day that last moved inside it.
- On a phone the toolbar is hidden: tap the left or right quarter of the screen to step a day, or drag the dot.

The site is updated every day with the latest complete UTC day.

## How the data is made

- **Balances.** Every balance change since the genesis block, from ethPandaOps Xatu's free public data (and a public
  Ethereum node where that data has gaps), rebuilt block by block and checked as it goes: every change must start from
  the balance rebuilt so far, to the wei, and the sum of all balances must stay equal to what was issued less what was
  burned and destroyed. Each account's balance is kept as a stack of lots: every rise is a lot stamped with the block
  it arrived in, and every fall spends the oldest lots first (FIFO).
- **Staked ETH, counted once.** ETH staked on the beacon chain is treated like any other balance: deposits come in as
  lots, withdrawals spend the oldest staked lots first, and the beacon chain's rewards come in as new lots on the day
  they are earned, so every day's bars add up to ETH's supply (Coin Metrics').
- **Prices.** Every coin carries the price when it last moved: Coin Metrics' daily closes, joined by a straight line
  through each day (from the day's open, the close the day before, to its close), at the moment it moved (to the 45
  minutes). $0 for the genesis allocation and for ETH last moved before 8 August 2015, the first day with a close.
- **Binning.** 625 equal-width bars from $0 to 0.1% past the highest close so far. Each day is cut into as few parts
  as keep ETH's move within each part to 0.5% of the price (up to 32); the coins of each part are spread over the
  prices that part of the day ran through, then blurred by a Gaussian of 0.24% of the price; total supply and value
  are kept exactly.

## This repository

The files that run the site, in minified form: the page, the build of its data and the workflows that publish it. The
source code is not public.

## Security

The page runs only its own scripts (each inline script is named by its hash in the Content-Security-Policy, and
Plotly is served by the site and pinned by its integrity hash), loads and connects to nothing but the site itself,
checks every data file before using it, and offers no file to download. It never asks you to install anything, connect
a wallet or type a seed phrase: anything that does is not this site. A check four times a day compares the live site
with this repository.

## Credits

Powered by ethPandaOps Xatu & Coin Metrics. Charts drawn with Plotly.js (MIT License); type set in Source Code Pro
(SIL Open Font License).

## License

Copyright (c) 2026 renshuBTC. All rights reserved (see LICENSE). The data belongs to its providers.
