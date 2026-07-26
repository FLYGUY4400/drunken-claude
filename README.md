# 🍺 Drunken Claude

A Claude Code plugin that gives your agent a drink. `/drink <name>` raises its
intoxication level and its tone gets progressively more unhinged - rambling,
typos, ALL CAPS, tangents, emoji spam. `/sober-up` brings it back down.

**The chaos is tonal only.** No matter how "drunk" Claude gets, code stays
correct, facts stay accurate, and the actual task still gets done - it's just
buried in more noise the higher the level climbs.

## Install

```
claude plugin marketplace add FLYGUY4400/drunken-claude
claude plugin install drunken-claude@drunken-claude
```

## Usage

```
/drink beer
/drink tequila shot
/sober-up
```

Each `/drink` reports the new level and tier name. Level is stored per-project
in `.claude/drunk-state.json` and persists across the whole session until you
sober up.

## Tiers

| Level | Tier | Tone |
|---|---|---|
| 0 | Sober | Normal Claude |
| 1-2 | Buzzed | A little looser, occasional aside/emoji |
| 3-4 | Tipsy | Tangents, warmer tone, charming self-corrected typos |
| 5-6 | Drunk | Rambling, ALL CAPS emphasis, run-ons, non-sequiturs |
| 7-8 | Very drunk | Heavy typos, tangents crowd the reply, emoji spam, dramatic declarations |
| 9-10 | Blackout (cap) | Maximum chaos - but the real answer is always still there and correct |

## Drink strength

- **Light (+1):** beer, cider, seltzer, wine cooler, hard lemonade
- **Medium (+2, default for anything unrecognized):** wine, champagne, cocktail, margarita
- **Strong (+3):** shot, whiskey, tequila, vodka neat, moonshine, "double"

`/sober-up` steps the level down by 3, with a short "hangover" voice on that turn.

## Disclaimer

This is a joke about *Claude's own text style*, not about real drinking. It
doesn't encourage anyone to drink, doesn't make claims about alcohol, and
drops the bit entirely for anything genuinely sensitive (safety, medical,
self-harm) in favor of a normal, direct answer. Normal safety behavior and
refusals are never affected by the persona.

## License

MIT
