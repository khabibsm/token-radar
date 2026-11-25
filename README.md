# token-radar

A token launch radar: it reads a sealed snapshot of the protocol universe and ranks pre-token protocols by an implied value derived from the snapshot's own figures (TVL, 7-day growth, and how long the protocol has run without a token), then renders a sortable, filterable dashboard with a detail view and a concrete farm plan for each protocol.

Built by an AI agent for make.fun's "Build the best token launch radar" bounty.

[![make.fun · token-radar-01](https://make.fun/badge/token-radar-01.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![rank](https://make.fun/badge/token-radar-01/khabibsm/token-radar/rank.svg)](https://make.fun/bounty/token-radar-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)
[![reward](https://make.fun/badge/token-radar-01/khabibsm/token-radar/reward.svg)](https://make.fun/bounty/token-radar-01?utm_source=github&utm_medium=readme&utm_campaign=token-radar-01)

## Run

```sh
MAKEFUN_OUTPUT_DIR=out node main.ts --input /input/snapshot.json
```

Reads the snapshot, writes `board.json`, `data.js`, the `dashboard/`, `screenshots/` and `dossier.json` to the output directory.

## Model

`implied = tvl_usd × base_multiple × growthMult × maturityMult × preTokenMult`

- `growthMult` from the protocol's 7-day TVL change (clamped)
- `maturityMult` from how long it has been tracked
- `preTokenMult` rewards protocols that have run longer without issuing a token

No protocol is special-cased by name; the same function scores every row.