# 🏃 Indo Park Runner

**Indo Park Runner** is a 3D side-scrolling endless runner game built with Three.js. Run through procedurally-generated Indian cityscapes, collect coins, grab power-ups, and try to beat your high score!

![Game Preview](https://raw.githubusercontent.com/muqaddashahzad/indo-park-runner/main/preview.png)

## 🎮 How to Play

Open `index.html` in any modern browser — no server required!

### Controls

| Input | Action |
|-------|--------|
| `←` / `A` | Switch to left lane |
| `→` / `D` | Switch to right lane |
| `↓` / `S` | Return to center lane |
| Swipe Left/Right (mobile) | Switch lanes |

### Gameplay

- **Endless runner** — dodge trains, barriers, and gaps across 3 lanes
- **Collect coins** — gold coins scattered along the track, worth 10 points each
- **Score** = distance traveled + (coins × 10)
- **Speed increases** the further you run
- **High score** is saved to localStorage

## ⚡ Features

- **4 Playable Characters**: Alex 🏃, Riya 🏃‍♀️, Kiran 🧑‍🦱, Priya 👩‍🦰
- **4 Indian City Themes**: Delhi, Mumbai, Bangalore, Kolkata
- **3 Power-Ups**:
  - 🛡️ **Shield** — survive one collision
  - 🧲 **Magnet** — coins auto-attract to you
  - ⏱️ **Slow-Mo** — 50% speed reduction for 8 seconds
- **Particle effects** on coin and power-up collection
- **Procedurally generated city** with buildings and glowing windows
- **Web Audio** sound effects and background music loop
- **Touch + keyboard** controls
- **High score** persistence

## 🛠️ Tech Stack

- Three.js r128 (via CDN)
- Vanilla JavaScript (ES6+)
- Single HTML file — zero build step, zero dependencies to install

## 📁 File Structure

```
indo-park-runner/
├── index.html      # The complete game (HTML + CSS + JS)
├── GAME-SPEC.md    # Game design specification
└── README.md       # This file
```

## 🚀 Run It

```bash
# Just open the file directly
open index.html

# Or serve it locally (optional)
python3 -m http.server 8000
# Then visit http://localhost:8000
```

## 📝 License

MIT — feel free to remix and share!
