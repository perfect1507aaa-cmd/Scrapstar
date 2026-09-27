# SPAZ-style prototype — research summary & build plan

Goal: a single `index.html` (canvas 2D, no external assets) that looks and plays as close as possible to
*Space Pirates and Zombies* (2011), judged against a reference gameplay screenshot. A reviewer agent scores
every build; the loop continues until the score is **9/10 or higher**.

## Team
| Role | Job |
|---|---|
| Gameplay researcher (agent) | controls, resources, combat model, fleet, AI, structure of a session |
| Art/UI researcher (agent) | palette from the reference screenshot, HUD layout in pixels, sprite/FX direction |
| Builder (main session) | writes the game, renders screenshots with a headless browser |
| Reviewer (agent) | compares screenshots + code with the reference, scores 1–10, lists the top fixes |

## Key findings (gameplay)
- Nose always turns to the cursor; **WASD thrust is relative to the ship** (forward 100%, reverse ~66%, strafe ~50%), inertia, **X = stabilisers**, **Shift = lock rotation**. No afterburner.
- **LMB** fires beams + cannons (cannons fire in a left-to-right *cascade*), **RMB** fires launchers. Everything drains a **reactor** pool shown as a ring of wedges around the cursor, with a *LOW POWER* warning.
- Damage layers: **shield bubble → 4 armour plates (front/left/right/rear) → hull**. Beams beat shields, cannons beat armour, missiles beat hull.
- Loot: **Rez chunks** (decay and split over time, fill the cargo hold, must be delivered to the **Warp Beacon**), **escape pods** (goons/crew), **Data orbs** (auto-drift to ships, level-ups give research points).
- Fleet of **3 ships**, number keys switch the piloted ship, wingmen AI, a pause **Tactics** screen (Space) with orders and research.
- Destroyed ships release a **white shockwave ring** that damages nearby ships. Ships don't collide.
- Factions by colour: player **blue**, UTA **red**, civilians **green**, zombies **purple**. Zombie *critters* swarm ships, eat shields, board and convert them.
- Off-screen ships are shown as **octagon markers** on the screen edge, coloured by relation, growing as they approach.

## Build plan
1. **Engine** — fixed-step loop, input, camera following the ship, headless test hooks (`?test=1`).
2. **Art generated in code** — domain-warped golden nebula, mottled sun with corona and filaments, painted metal ship sprites (plates, seams, grime, bevels, faction trims, lit windows), dark derelict hulks, rez chunks, data orbs.
3. **Flight & combat** — ship-relative thrust, mass/turn rates, shields → armour facings → hull, beams / cascade cannons / homing missiles, reactor energy.
4. **Loot & economy** — decaying rez, cargo hold, warp beacon delivery, pods → goons, data → research points.
5. **Fleet & AI** — 3-ship fleet with number-key switching, wingmen follow/attack, enemy AI (UTA, civilians, zombies + critters), flee behaviour.
6. **HUD** — REZ / GOONS / DATA bars, UPGRADE POINTS, circular ship-status gauge (armour ring segments, shield & hull numbers), cargo & crew lines, fleet slots 1–3 on the left, octagon buttons on the right, cursor reticle with energy wedges, off-screen markers.
7. **Juice** — explosions with fire, smoke, sprite fragments and shockwaves; shield-hit arcs; beam muzzle fire; screen shake; synthesised sound.
8. **Review loop** — render 4 screenshots per build → reviewer scores vs. the reference → fix the top issues → repeat until ≥ 9/10.
