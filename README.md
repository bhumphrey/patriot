# We The People

A first-person browser game about defending the U.S. Capitol at dusk. A shambling crowd pours across the National Mall toward the steps: some in red caps, a few waving blue flags. Behind them, the floodlit Washington Monument, the Lincoln and Jefferson Memorials, the White House, and the Smithsonian line the skyline. Your only weapons are the founding documents and the flag.

**▶ Play it: https://bhumphrey.github.io/patriot/**

Hit a zombie with the Constitution or the Declaration and it comes to its senses. The cap falls off, the flag drops, and it turns around and walks home. Nobody gets hurt. Let too many reach the steps and the Republic falls.

## How to play

Keep the crowd off the Capitol steps. Each zombie that gets through costs **Integrity of the Republic**. When it hits zero, the chamber is breached.

### Weapons

| Key | Weapon | How it works |
|---|---|---|
| `1` | **The Constitution** | Fast, flat, and precise. One hit converts a zombie. |
| `2` | **Declaration of Independence** | Slower and heavier, but hits a much wider area. Good for a packed lawn. |
| `3` | **Old Glory** (melee) | Sweeps everyone within about 5 m in front of you. Each swing knocks them back and staggers them, and **three swings** convert a zombie. |

### Controls

| | Desktop | Phone / tablet |
|---|---|---|
| Move | `W` `A` `S` `D`, hold `Shift` to run | Drag the thumbstick on the left. Push it to the rim to run. |
| Look | Mouse | Drag anywhere on the right |
| Throw / swing | Left click (hold to keep firing) | Hold the gold button. Slide your thumb to aim while firing. |
| Switch weapon | `1` `2` `3`, or `Q` to cycle | Const. / Decl. / Flag buttons |
| Mute music | `M` | ♪ button |
| Release mouse | `Esc` | n/a |

On a phone, the game plays best held sideways.

### Waves and scoring

Waves get bigger and faster. From wave 4, **runners** appear: faster zombies in dark red, hunched further forward. You score for every zombie converted, with bonuses for dropped caps, lowered flags, and runners. Your personal best is saved in your browser.

Converted zombies leave their regalia on the ground. **Walk over a dropped cap, banner, or headdress to collect it** for bonus points: 5 for a cap, 12 for a banner, 50 for the Shaman's headdress. Your running tally is under the score.

Regalia doesn't lie there forever. A drop lasts **26 seconds in wave 1 and 2 seconds less every wave**, down to a floor of 7, and it blinks and shrinks before it goes. Later waves make you choose between chasing the regalia and holding the line.

### The Shaman

Every **five minutes**, the **Shaman** comes up the Mall in a buffalo-horn headdress. The countdown is shown under the wave number. One page won't turn him back: every document hit or flag swing takes one point off his health bar. Beat him and the headdress comes off, worth 260 points, and you can collect it from the ground for 50 more. Let him reach the steps and the Republic loses 30 Integrity.

## The music

The soundtrack is an original march, synthesized live in the browser (no audio files). It follows the danger level:

- **Horde away:** a bright major key at 118 bpm, with brass, tuba oom-pah, snare, cymbals, and glockenspiel.
- **Closing in:** the same tune turns minor, with darker brass and tom rolls.
- **At the steps:** doom. The tempo drags toward 86 bpm, the brass drops an octave, and the drums become a heartbeat under timpani and a low drone that grows dissonant when things are dire.

Danger is measured from how many zombies are advancing, how close the nearest one is, how much Integrity you've lost, and whether the Shaman is on the field.

## Running it locally

Everything is in one file, [`index.html`](index.html), with no build step. Open it in a browser:

```bash
open index.html
```

The only external dependency is [Three.js r128](https://threejs.org/), loaded from cdnjs, so you need an internet connection. To serve it the way GitHub Pages does, run a local web server instead:

```bash
python3 -m http.server 8777
```

Then visit http://localhost:8777.

## How it's built

- **Rendering:** Three.js with procedural geometry for everything: the Capitol, the zombies, the parchment, and the flag cloth. Textures are drawn to canvas at startup. There are no image files.
- **Audio:** Web Audio API. Sound effects and the march are synthesized from oscillators and filtered noise, and the music engine schedules notes slightly ahead of time so the timing stays tight.
- **Input:** Pointer Lock for mouse-look, with a right-drag fallback where pointer lock isn't allowed. Pointer Events handle multi-touch on phones.
- **Leaderboard:** the game can keep a shared leaderboard when hosted as a Claude artifact. Anywhere else, including GitHub Pages, it shows each player's own best score from local storage.
