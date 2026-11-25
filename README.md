# Token Radar: Pre-Token Protocol Rankings

A static dashboard that ranks pre-token DeFi protocols by implied value using a transparent model. The watchlist forms the floor (protocols with ≥ $50M TVL and no token), and the early radar adds 160 pre-token protocols below that floor, ranked by TVL.

## Model

The implied value is computed as:

```
implied = round(
  tvl_usd × 0.25
  × (1 + clamp(change_7d, -60, 120) / 100 × 0.5)
  × (1 + min(age_days, 1095) / 1095 × 0.25)
  × (0.6 + min(age_days, 1095) / 1095 × 0.4)
)
```

- **base_multiple**: 0.25
- **growth_weight**: 0.5 (clamped to [-60%, 120%])
- **pretoken_weight**: 0.25 (rewards protocols that have run longer without a token)
- **maturity**: 0.6–1.0 (capped at 3 years)

No protocol name is ever special-cased.

## Run

```bash
mkdir -p out
MAKEFUN_OUTPUT_DIR=out node main.ts --input /root/makefun/token-radar-01-kit/input/snapshot.json
```

Outputs `out/board.json`, `out/data.js`, `out/dashboard/`, `out/screenshots/`, and `out/dossier.json`.

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/khabibsm/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard)
[![reward](https://make.fun/badge/token-radar-01/khabibsm/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01)