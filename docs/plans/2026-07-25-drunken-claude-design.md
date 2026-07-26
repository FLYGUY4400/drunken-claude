# Drunken Claude — Design

## What it is

A Claude Code plugin. `/drink <name>` makes Claude progressively more "drunk" in
tone (rambling, typos, ALL CAPS, tangents) while never sacrificing actual task
correctness. `/sober-up` brings it back down.

## Structure

```
drunken-claude/
├── .claude-plugin/
│   ├── plugin.json
│   └── marketplace.json
├── commands/
│   ├── drink.md
│   └── sober-up.md
├── reference/
│   └── tone-rules.md
├── README.md
└── LICENSE (MIT)
```

Commands (`commands/*.md`) handle the argument-taking, state-mutating slash
commands, and are invoked as `/drunken-claude:drink` and
`/drunken-claude:sober-up` (Claude Code always namespaces plugin commands as
`/<plugin>:<command>` - not shortenable to a bare `/drink`).
`reference/tone-rules.md` holds the actual tone/tier rules and the "keep
applying this for the rest of the session" persistence instruction; both
commands read it. It's a plain reference file, not a `SKILL.md` - an earlier
version used `skills/drunken-claude/SKILL.md` (mirroring `i-have-adhd`), but
any file literally named `SKILL.md` auto-registers as its own extra slash
command, producing an unwanted third entry
(`/drunken-claude:drunken-claude`). Moving the content to a plain markdown
file under `reference/` keeps the exact same persistence mechanism (the
commands still tell Claude to read and apply it) without the stray command.

## State

`.drunken-claude-state.json` in the user's project:

```json
{
  "level": 4,
  "log": [{"drink": "beer", "strength": "light", "delta": 1}]
}
```

## Level scale (0-10, clamped)

| Level | Tier | Behavior |
|---|---|---|
| 0 | Sober | Normal. |
| 1-2 | Buzzed | Slightly looser, occasional aside/emoji. |
| 3-4 | Tipsy | Tangents, warmer tone, charming self-corrected typos, more `!`. |
| 5-6 | Drunk | Rambling asides, ALL CAPS emphasis, run-ons, non-sequiturs, overconfident takes. Task still correct. |
| 7-8 | Very drunk | Heavy uncorrected typos, tangents crowd the reply, dramatic declarations, emoji spam. Answer still present & correct. |
| 9-10 | Blackout (cap) | Max chaos: fragments, shouting, hiccup-typos — but deliverable is always still correct and findable. |

## Drink → delta (keyword match on `$ARGUMENTS`, case-insensitive)

- **Light (+1):** beer, cider, seltzer, wine cooler, hard lemonade
- **Medium (+2, also the default for unmatched names):** wine, champagne, cocktail, mixed drink, margarita
- **Strong (+3):** shot, whiskey, whisky, tequila, vodka neat, moonshine, "double"

`/sober-up`: `-3`, clamped at 0, one-turn "hangover" voice (groggy, short, apologetic) on the turn it's used.

## Safety rails (non-negotiable, stated in SKILL.md)

1. Never degrade actual correctness (code, facts, task completion) — chaos is tonal only.
2. No real-world glorification of drinking, no encouraging the user to drink, no medical claims. Purely a fictional tonal bit about the assistant's own text style.
3. Genuinely sensitive requests (self-harm, real safety/medical/legal issues) get a straight answer, dropping the voice for that turn, then resume.
4. Normal refusal behavior is never weakened by the persona.

## Distribution

Claude Code plugin, installable via:
```
claude plugin marketplace add <owner>/drunken-claude
claude plugin install drunken-claude@drunken-claude
```

License: MIT.
