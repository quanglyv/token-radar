[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/quanglyv/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/quanglyv/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
# Token Radar — make.fun bounty `token-radar-01`

Build the best token launch radar. Deadline: 17:00 Mon 14 Dec 2026 (+07).
Prize: $1,325 split across the top 10 (1st $1,000). An AI judge compares
dashboards pairwise; places go by win rate.

## What it is

A static dashboard that ranks the protocols in DefiLlama's sealed snapshot
which record **no token yet**, by what their launch would be worth under one
stated model (`radar-2`). It scores **198 rows**: the whole 40-protocol
watchlist plus every other eligible pre-token protocol below the $50M floor.
Wrapped, staked and bridged products of tokens that already trade, exchanges
and versioned pools are left out, because their launch would not be a new
token. Protocols whose token already trades are shown apart, with their real
market cap, never mixed into the ranking.

Model (`radar-2`, in `lib/model.ts`):

```
implied = round( tvl_usd x 0.25
  x (1 + clamp(change_7d, -50, 100) / 100 x 0.6)
  x (0.70 + min(age_days, 1095) / 1095 x 0.30)
  x (1 + 0.02 x min(chains - 1, 5)) )
```

TVL is the size of the economy a token would tax; 7-day growth is momentum;
age is how long the protocol has run with no token; chain breadth is a small
credit for serving more than one chain. No protocol name is special-cased.
Each row carries a six-step farm plan with cost and time, derived from its
category, chains, TVL and age.

## Data

The snapshot is the kit's sealed input, `input/snapshot.json`: DefiLlama
`https://api.llama.fi/protocols`, fetched **2026-11-14T01:18:33Z**, 758
protocols at or above $5M TVL, floor $50M, watchlist 40. It is frozen: the
grader runs this program twice in a sandbox with no network against the same
bytes, so the program reads only that file. (A live fetch was considered and
rejected: the gate only accepts slugs from the sealed snapshot, which holds
758 protocols, so a 1,000–4,000-row board from live data could not pass.)

## Run it

```sh
mkdir -p out && MAKEFUN_OUTPUT_DIR=out node main.ts --input input/snapshot.json
```

Node 22.18+ (tested on Node 24.22.1), standard library only, no install.
Output: `board.json` (`{"rows": [...]}`), `data.js`, `dashboard/`,
`screenshots/` (3), `dossier.json` (via the kit's vendored
`vendor/makefun-board.ts`, byte for byte). The dashboard is static and makes
no network calls; open `out/dashboard/index.html` in a browser. Dashboard
source totals ~40 KB, inside the 65,536-byte dossier text cap.

## Layout

- `main.ts` — entry program: snapshot in, board + dashboard + dossier out
- `lib/model.ts` — radar-2 model, board builder, farm plans, snapshot parser
- `vendor/makefun-board.ts` — make.fun's dossier library, kit copy verbatim
- `dashboard/` — `index.html`, `app.css`, `app.js` (search, category/chain/
  age/growth filters, sorting, detail view, live-token tab, model panel)
- `screenshots/` — `1-board.png` (board), `2-detail.png` (detail view),
  `3-filtered.png` (filtered view), all 1440x800
- `dossier/report.md` — the dossier: what the radar shows, sources, scoring
- `input/snapshot.json` — sealed kit snapshot, local test fixture only; the
  grader mounts its own copy at `/input/snapshot.json`

## Submission (not done here — no repo created, nothing pushed, no wallet connected)

- Intended repo: to be created under `github.com/quanglyv/` (user's GitHub is
  **quanglyv**). The repo must be created after the bounty opened and must
  belong to that account.
- Payout wallet (Solana, USDC): `A7Vi7oZyDdw7xaoRfckwkyfxz1NT4XStrRC5Hs4Ea2Yp`
- To submit, the parent agent runs the kit's record/submit flow from a
  session on that GitHub account, with the Solana wallet linked for signing
  and claiming. This build does not connect, sign or submit anything.
