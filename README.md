# 🍺 Drunken Claude

A Claude Code plugin that gives your agent a drink. `/drunken-claude:drink <name>`
raises its intoxication level and its tone gets progressively more unhinged -
rambling, typos, ALL CAPS, tangents, emoji spam. `/drunken-claude:sober-up`
brings it back down.

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
/drunken-claude:drink beer
/drunken-claude:drink tequila shot
/drunken-claude:sober-up
```

(Plugin commands are always namespaced as `/<plugin>:<command>` by Claude Code
to avoid collisions between plugins - this isn't shortenable to a bare `/drink`.)

Each `/drink` reports the new level and tier name. Level is stored per-project
in `.drunken-claude-state.json` and persists across the whole session until you
sober up. It's local, per-user session state, so you'll probably want to add
`.drunken-claude-state.json` to your project's `.gitignore`.

You'll see the underlying `Read`/`Write` tool calls in your terminal when you
run these commands - that's normal Claude Code transparency for any command
that touches files, not something this plugin can or should hide.

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
