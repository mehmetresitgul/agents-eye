# agents-eye

A skill that makes coding agents decide where the eye goes before they write any UI.

```
npx skills add mehmetresitgul/agents-eye
```

> **Read `SKILL.md` before installing.** A skill is instructions your agent will follow. Know what it tells the agent to do.

## What it does

Agents produce interfaces that look the same because they never decide anything: default font, centered hero, purple gradient, three equal cards. agents-eye forces the decisions first, applies a measured system, then checks the result with numbers.

## Why

Most agents produce interfaces without judgment.  
agents-eye exists to make judgment non-optional.

The constraints are derived from how the human visual system and brain actually process information: attention, cognitive load, hierarchy, and the mathematics of proportion.  
Golden ratio relationships, Swiss discipline, spacing rhythm, and type scale are not stylistic preferences. They are measurable outcomes of how the eye moves and how the mind organizes what it sees.

Every rule is grounded in the psychology of perception and the neurology of visual attention.  
No defaults. No trends. Only decisions that can be justified.

The agent decides first. Then it designs.

## When it triggers

Landing pages, heroes, marketing and product sites, portfolios, any UI screen: building, redesigning or critiquing. Also when the request is "make it look designed", "less AI", "YC style" or "like Linear / Vercel / Stripe".

## Protocol

1. **Eye path.** Pick a template (A–E), write the 1st / 2nd / 3rd focus with numbers, name the element that competes with the 1st and how it is suppressed. No code before this.
2. **System.** Type scale on φ, spacing in multiples of 8px (with a 4px micro step), 12-column grid at 1440, at most 2 fonts, one saturated color for one action.
3. **Code.**
4. **Audit.** Run the first-screen script in the browser console, or the static grep commands. A flag means "justify it", not "reject it".

## Contents

| File | Purpose |
|---|---|
| `SKILL.md` | Protocol and hard rules |
| `references/eye-path.md` | Templates A–E, pre-code block, validation tests |
| `references/swiss-system.md` | Type scale, spacing, grid, radius tokens |
| `references/type-and-color.md` | Font pairings, banned fonts, color rules |
| `references/anti-ai.md` | Measurable bans, audit script, grep checks |

## Measurements

The 48 references were measured in a browser at 1440×900 on **23 November 2026**. Sites change; treat the numbers as a snapshot and re-measure before relying on one.

## License

MIT. See `LICENSE`.
