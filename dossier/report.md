# Token Radar — dossier

## What the radar shows

A ranked board of the 198 protocols in the sealed snapshot that record no
token yet, once wrapped, staked and bridged products of tokens that already
trade, exchanges and versioned pools are left out. It covers the whole
40-protocol watchlist and adds 158 eligible protocols below the $50M floor.
Each row shows TVL, seven-day TVL growth, age with no token, chains, risk
flags and an implied value, plus a six-step farm plan with cost and time.
Protocols whose token already trades are shown apart, with their real market
cap, never mixed into the ranking. The dashboard is searchable, filterable by
category, chain, age and growth, sortable, and every row opens a detail view
that recomputes its implied value in the page and checks it against the
board. Nothing on the page fetches the network.

## Data sources

One source only: the sealed snapshot of 14 November 2026 from the DefiLlama
protocol index (758 protocols at or above $5M TVL, fetched
2026-11-14T01:18:33Z). The snapshot is frozen, so every figure the board
shows comes from those bytes. "No token" means the snapshot records no
token; a protocol may still have a token its record does not carry.

## Scoring (model radar-2)

Implied value = TVL x 0.25, times a growth multiplier (seven-day change,
clamped to -50%..+100%, weighted 0.6), times a maturity multiplier (0.70 to
1.00 over three years of age), times a breadth multiplier (+2% per extra
chain, up to five). One function scores every row; no name is special-cased.
A missing seven-day change scores as zero growth and an unknown listing date
as 365 days, so no row is dropped for a gap. The top row is Steakhouse
Financial, about $634M implied; the board's implied values run from there
down to about $0.8M. Implied value is the radar's own claim, never a price
and never a prediction that a token launches.

## How to read it

Start at the top: the largest implied values are the largest economies a
token would tax. Use the growth filter to find momentum and the age filter
to separate new protocols from ones that have run for years with no token.
Read the flags: falling TVL, under 90 days old, single chain and missing data
are reasons to look closer, not reasons to buy. Open a row before farming
it: the detail view shows the exact multipliers and the plan's cost and
hold time. Farming costs gas and carries smart-contract risk; claim only
from links the protocol itself publishes, and never pay to claim.

## Submission

Intended repo under github.com/quanglyv/ (GitHub user quanglyv). Payout
wallet (Solana, USDC): A7Vi7oZyDdw7xaoRfckwkyfxz1NT4XStrRC5Hs4Ea2Yp. This
build creates no repo, pushes nothing and connects no wallet.
