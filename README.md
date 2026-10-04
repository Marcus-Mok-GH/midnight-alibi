# 🕯️ Midnight Alibi

An AI-hosted, pass-and-play **social deduction party game**. One phone, 4–12 players
around a table. An AI host invents a brand-new mystery every game, deals every player
a secret role, narrates each round's twists, runs the discussion timer and reads out
the votes aloud.

**Play:** https://marcus-mok-gh.github.io/midnight-alibi/

Built as a submission for the Pollinations quest *Party deduction game with an AI
host* (#15726).

## Why it's fair

**The game engine decides everything; the AI only writes the story.**

- Roles are dealt to players with a crypto-random shuffle *after* the AI writes the
  role cards: the AI never knows who holds which card, so it can never leak the
  culprit.
- Votes are tallied in code. Ties eliminate nobody. The winner is decided in code.
- The host's only job is atmosphere: the scenario, the round beats, the tally
  read-out and the epilogue.

## Features

- **Pass-and-play on one device**: privacy screen with *hold-to-reveal* secret role
  cards, so nobody peeks by accident.
- **A new scenario every game**: setting, incident, culprit and innocent role cards
  with distinct clues and personal objectives, generated live by the AI host.
- **Narration aloud**: every beat is spoken with text-to-speech (voice picker); a
  discussion timer with countdown beeps; the vote tally is read out dramatically.
- **Bring Your Own Pollen**: the host pastes their own Pollinations API key. It's
  stored only in the browser and sent only to `gen.pollinations.ai`. A whole game
  is a handful of small requests, typically well under 1 Pollen.
- **Works without a key too**: if no key is provided (or the host is unreachable),
  the game deals one of the built-in mystery scenarios so the party never stalls.
- Model and voice pickers load the **live Pollinations catalog**.

## How it uses Pollinations

| Call | Endpoint | Purpose |
|---|---|---|
| Scenario + role cards | `POST /v1/chat/completions` | fresh mystery each game |
| Round narrations, tally read-out, epilogue | `POST /v1/chat/completions` | dramatic host beats |
| Speech | `GET /audio/{text}?voice=…` | spoken narration |
| Model catalog | `GET /text/models` | host model picker |

## Run locally

It's a single static page. Open `index.html`, or serve the folder with any static
server. No build step, no dependencies.

Get a key at [enter.pollinations.ai/keys](https://enter.pollinations.ai/keys).

## Credits

Powered by [Pollinations](https://pollinations.ai): text, speech and the model
catalog all run on the Pollinations API.
