# Ledger — an idle game about small, deliberate trades

**[Play it live →](https://bob0929.github.io/paper/)**

A browser-based idle game built for Paper-App Studio. You gather paper, bind it into
ink and books, and trade everything through a market with prices that drift on their
own — but every trade is a click you choose to make, not something that happens for you.

---

## Why it works this way (design note)

The game's own **Design Note** card (visible in-app, at the bottom of the page) lays
out the actual reasoning, sourced from Hunicke, LeBlanc & Zubek's MDA framework:
automate the repetitive action (clicking Gather) but keep the one meaningful choice —
*when* to trade — entirely manual. The idea is that dynamics, not mechanics, are what
produce the felt experience, and a single retained decision point is what should keep
the game feeling active instead of like a spreadsheet ticking up on its own.

I'm flagging in that same note that this is untested against a real player. That's
what the observation below is for.

## What's actually in the build

- **Resources** — Paper (manual gather), Ink and Books (auto-produced by upgrades,
  gated behind lifetime-collected thresholds so they don't all dump on screen at once)
- **Market** — every resource has a coin value that drifts between 0.7x–1.4x on a
  randomized timer, eased rather than snapped, so prices feel like drift, not noise.
  Trades are full-stock, single-click, and entirely player-initiated.
- **Upgrades** — exponential cost curve, split between rate upgrades (passive
  production) and click upgrades (bigger manual gathers)
- **Achievements** — six of them, checked live every tick against real game state,
  two of which grant a permanent click-yield bonus
- **Procedurally generated Orders** — a single active delivery contract at a time,
  regenerated (slightly bigger) every time it's fulfilled, paying above market rate
  on purpose as the incentive to seek them out
- **Staged onboarding** — most cards are hidden behind a real gather → sell → upgrade
  sequence; returning players with an existing save skip straight past it
- **On-demand hints** — a `?` button that re-evaluates a rule list against live state
  every time it's clicked, so the advice is always targeted at where you actually are
- **Persistence** — saves to `localStorage`, restores on load, and simulates offline
  production (capped at 8 hours) using the exact same production function the live
  loop calls, so there's no separate offline-math path to keep in sync
- **Light/dark theme toggle**

## What isn't true (so I don't oversell it)

This is a single `index.html` file. Comments throughout label sections with intended
future homes (`src/core/state.js`, `src/systems/production.js`, etc.) — that's a note
to future-me about how I'd split it up, not a real file structure. There is no build
step, no modules, no framework. One file, vanilla JS, by design for this assignment.

## A revision I can actually point to

Early on, the Market had a flat automatic-sell rate. I pulled it because it quietly
removed the only decision the player had left — see the code comment above
`tradeFullStock` in the `Systems.Market` object for the reasoning at the time. Every
trade in the current build requires a click.

`[FILL IN — were there other revisions? Onboarding, achievements, or hint logic that
changed shape after you built a first version? List them with a short before/after,
or say plainly if this was the only one.]`

## Reader observation

`[FILL IN — this is the actual assignment deliverable and I'm not writing it for you.
Watch one real person play this cold, with no explanation from you. Note: where they
got stuck, what they clicked expecting something different to happen, whether the
onboarding banner actually got read, whether they noticed the price drift or ignored
it. Then say what you changed (or would change) as a result, and why.]`

## Running it locally

No build step. Clone the repo and open `index.html` in a browser, or serve the folder
with any static server (e.g. `python3 -m http.server`) if you want it at a proper URL
instead of `file://`.

## Credits

MDA framework: Hunicke, R., LeBlanc, M., & Zubek, R. (2004). *MDA: A Formal Approach
to Game Design and Game Research.* [users.cs.northwestern.edu/~hunicke/MDA.pdf](https://users.cs.northwestern.edu/~hunicke/MDA.pdf)

Built by Henry (bob0929) for Paper-App Studio.
