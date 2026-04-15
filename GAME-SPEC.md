# Indo Park Runner — Game Specification

## Project Status
**Current:** Working prototype (v1) — side-scrolling 3D endless runner
**Goal:** Full-featured 3D game promoting India-Pakistan harmony/love

## Current Implementation (v1 Prototype)
- **File:** `/home/open-claw/indo-park-runner/index.html`
- **Size:** 32KB, 902 lines
- **Tech:** Three.js r128, single HTML file, CDN imports
- **GitHub (old games):** `https://github.com/muaddashahzad/indo-pak-love`
- **Live (old):** `https://muqaddashahzad.github.io/indo-pak-love/`

## Game Architecture

### Tech Stack
- Three.js r128 via CDN: `https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js`
- No build step — single HTML file
- No external assets — all geometry procedurally generated
- localStorage for high score persistence

### Core Game Loop
```
menu → select (character + city) → playing → gameover → menu
```

### Current Features
- 3D side-scrolling endless runner (Subway Surfers style)
- 3 lanes (left/center/right)
- Character selection (4 plain capsule characters)
- City selection (4 cities with color themes)
- Obstacles (trains, barriers, gaps)
- Collectible coins
- Score + distance tracking
- High score persistence
- Touch swipe + keyboard controls
- Mobile responsive

### Three.js Scene Setup
- Camera: `PerspectiveCamera(75, aspect, 0.1, 1000)` at `(-8, 5, 0)` looking at `(5, 1, 0)`
- Renderer: `WebGLRenderer` with `antialias: true`, pixel ratio capped at 2
- Fog: `THREE.Fog` per-city color, near=50, far=150
- Lighting: AmbientLight (0xffffff, 0.6) + DirectionalLight (0xffffff, 0.8) at (10, 20, 5)
- Shadow: enabled on directional light, 1024x1024 map

### Player Character (Procedural Capsule Human)
- Body: `CapsuleGeometry(0.3, 0.8, 4, 8)` with character color
- Head: `SphereGeometry(0.25, 16, 16)` skin tone
- Eyes: small black spheres
- Arms: `CapsuleGeometry(0.1, 0.5)` same color as body
- Legs: `CapsuleGeometry(0.12, 0.5)` dark color
- Running animation: legs oscillate with `sin(playerLegAngle)`
- Lane switching: lerp toward `CONFIG.lanes[targetLane]` at 0.15 factor

### Obstacles
1. **Train** (40% spawn rate): `BoxGeometry(2, 2.5, 1.5)` dark + red horizontal stripes
2. **Barrier** (30%): `BoxGeometry(2.5, 0.8, 0.5)` orange
3. **Gap** (30%): `BoxGeometry(2, 0.1, 3)` dark, player must jump over

### Coins
- Geometry: `TorusGeometry(0.3, 0.08, 8, 24)` gold
- Inner detail: `CircleGeometry(0.2, 16)` gold circle
- Animation: rotation.x += 0.1, rotation.z += 0.05 per frame
- Collection: proximity check, remove from scene + array

### Environment (Per-City)
| City | Sky/Fog | Ground | Theme |
|------|---------|--------|-------|
| Delhi | #ffb74d | #8d6e63 | Warm orange |
| Mumbai | #4dd0e1 | #607d8b | Cyan/blue |
| Bangalore | #81c784 | #795548 | Green |
| Kolkata | #9575cd | #5d4037 | Purple |

### Buildings (Procedural)
- Two sides (left/right of track)
- Random height (8-28), width (5-13), depth (5-13)
- Color: random hue 0.55-0.65 (blue-green), saturation 0.3, lightness 0.4
- Windows: white/yellow `PlaneGeometry(0.8, 1.2)` on building faces
- Recycled when z > 50, reset to z -= worldLength * 2

### Ground
- Two `PlaneGeometry(20, 200)` segments
- Rotated -90° on X axis
- Recycled when z > worldLength

### Controls
- **Desktop:** Arrow keys (←↓→) or A/D keys
- **Mobile:** Touch swipe left/right (dx > 30px threshold)
- Lane 0 = left (-3), Lane 1 = center (0), Lane 2 = right (+3)

### Scoring
- Distance: increments by `speed * distanceMultiplier` per frame
- Score: `floor(distance) + (coins * coinValue)`
- `coinValue = 10`, `distanceMultiplier = 1`
- High score saved to `localStorage.indoRunner_bestDistance`

### Speed Progression
- Start: 0.5
- Increase: +0.00005 per frame
- No upper cap (infinite scaling)

### Collision Detection
- Bounding box check: `|obs.z| < 1.5 && |obs.x - player.x| < 1.2`
- Gap type exception: `player.y < 0.3` required to survive

---

## Future Vision (What Muqaddas Wants)

### Core Gameplay Changes
1. **Front-facing perspective** — camera behind player, depth toward screen (Subway Surfers true 3D)
2. **Real Indian city environments:**
   - **Lahore:** Badshahi Mosque, Minar-e-Pakistan, Lahore Fort, Wagah Border
   - **Delhi:** Taj Mahal, Red Fort, Qutub Minar, Chandni Chowk
   - **Mumbai:** Gateway of India, Marine Drive, Bollywood signs
   - **Karachi:** Clifton Beach, Mazar-e-Quaid, Port
   - **Amritsar:** Golden Temple
   - **Agra:** Taj Mahal
3. **PK/IN flag-themed characters** — player dressed in national flag colors
4. **City streets, train rails** — more authentic Subway Surfers feel

### Obstacles (Meaningful)
- Media vans spreading fake news
- Protest crowds / fanatics
- Jingoistic politicians giving hate speeches
- Soldiers / military presence
- Barriers representing division

### Player Actions
- Run (current)
- Jump (to avoid obstacles)
- **NEW:** Stop fights between people
- **NEW:** Protect innocent bystanders
- **NEW:** Spread peace messages

### Educational Elements
- Kashmir issue exploited for political gain
- War rhetoric and its consequences
- Real issues that divide the peoples
- Positive messaging about harmony

### Audio
- Real crowd sounds
- City ambience
- Event sounds (impacts, collecting items)
- Voice lines (cheers, peace messages)

### Technical Upgrades
- Real 3D assets (GLTF models for landmarks)
- Web Audio API for real sound
- More polished animations
- Sound effects + background music

### Monetization (Future)
- In-game advertising
- Premium features

---

## Old Abstract Games (IGNORE)
Location: `/home/open-claw/indo-pak-love/`
- IndoPak Runner (abstract side-scroller — WRONG direction)
- Bridge Builder
- Rhythm of Harmony
- The Dosti Diaries
- Clash of Hearts

These were the first attempt but don't match Muqaddas's vision. Focus on rebuilding Indo Park Runner with the real city/landmark vision.

---

## Notes for Next Session
1. Game file: `/home/open-claw/indo-park-runner/index.html`
2. Open in browser: `file:///home/open-claw/indo-park-runner/index.html` or serve with `python3 -m http.server 8080` in that directory
3. Current version is a working prototype — NOT the final vision
4. Muqaddas wants: real landmarks, front-facing camera, PK/IN themed characters, meaningful obstacles, real sounds, educational messaging
5. GitHub repo: `muqaddashahzad/indo-pak-love` (old games, needs new home for updated game)
6. Android SDK: `/home/open-claw/android-sdk/`
7. Capacitor setup available from KidsLearn Hub reference: `/home/open-claw/kids-learn-hub/android/`
