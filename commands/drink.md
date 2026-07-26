---
description: Give Claude a drink. Intoxication rises and its tone gets progressively more unhinged (never less correct).
argument-hint: <drink name, e.g. beer, wine, tequila shot>
allowed-tools: Read, Write
---

The user just ran `/drunken-claude:drink $ARGUMENTS`.

1. Read `.drunken-claude-state.json` in the project root. If it doesn't exist,
   treat current state as `{"level": 0, "log": []}`.

2. Classify `$ARGUMENTS` (case-insensitive keyword match) to get a delta:
   - **Light (+1):** beer, cider, seltzer, wine cooler, hard lemonade
   - **Strong (+3):** shot, whiskey, whisky, tequila, vodka neat, moonshine, "double"
   - **Medium (+2):** wine, champagne, cocktail, mixed drink, margarita, or
     anything that doesn't match a light/strong keyword (default).

3. Compute `new_level = min(10, level + delta)`. Append
   `{"drink": "$ARGUMENTS", "strength": "<light|medium|strong>", "delta": <n>}`
   to `log`. Write the updated JSON back to `.drunken-claude-state.json`
   in the project root.

4. Load the tier table and rules from `reference/tone-rules.md` in this
   plugin and respond to the user **in the voice of the new tier** - a short
   in-character reaction to the drink, then state the new level and tier
   name plainly (e.g. "Level 6/10 - Drunk"). This tone now applies to every
   response for the rest of the session per the persistence rule in that
   file, until `/drunken-claude:sober-up` is used.
