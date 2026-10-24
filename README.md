# PIGEON BRO: MEETING MAXIMALIST

**One workday. Zero decisions. Infinite syncs.**

A single-file browser game about a pigeon in a black turtleneck who is also a billionaire tech founder. Your only job is to attend as many pointless Zoom meetings as possible between 9:00 AM and 5:00 PM, and to screen-share the most deranged PowerPoint deck you can find in a dropdown.

```
pigeon_bro_1.html       ← the game (landscape stage, desktop / laptop)
pigeon_bro_phone.html   ← the same game, portrait layout for phones
```

---

## Play it

Open `pigeon_bro_1.html` in any modern browser (Chrome, Edge, Firefox, Safari). Double-clicking the file works — there is no server, no build step, no install, and no network access required.

The game renders on a fixed 1280×720 stage that scales to fit your window, so it looks the same on a laptop or a 4K monitor. Sound is synthesized live with WebAudio and starts on your first click.

**A run takes about 3–5 minutes.** Then you get a rank, and the option to clock in again.

---

## Phone version

`pigeon_bro_phone.html` is the same game rebuilt for a portrait screen. Same rules, same 32 meetings, same 31 decks, same scoring, same achievements — the layout is what changed.

- **Stage is 720×1560 (≈9:19.5)**, so it fills the screen edge to edge on a modern phone (iPhone 13/14, Galaxy S22, Pixel 7) with no letterboxing on the dominant sizes.
- **Bottom-sheet invites.** The invite card comes up from the bottom of the screen with full-width thumb-sized buttons (60+ px tall) instead of a card floating on the right.
- **The call is stacked vertically:** meeting title, your webcam tile with the pigeon in it, engagement bar, buzzword chips, a 3×2 attendee grid, then NOD / BUZZWORD across the bottom where your thumb already is.
- **Touch first.** Buttons fire on `touchstart` (no 300 ms tap delay), with a short haptic tick via the Vibration API where the device supports it. The deck choices are 140 px cards. Keyboard shortcuts still work if you plug in a keyboard.
- **Landscape guard.** Held sideways, a phone shows a "rotate your phone" card and pauses the game instead of shrinking it into a 180 px strip.
- Uses `visualViewport` for sizing, so the iOS/Android URL bar collapsing doesn't crop the stage, and sets `viewport-fit=cover` with no zoom, no rubber-band scrolling and no tap highlight.

Open it the same way — no server, no install. On iOS Safari or Chrome on Android you can also "Add to Home Screen" and it runs full-screen.

---

## The pitch

You are a pigeon. You are a billionaire. You have a lanyard that says CEO and 32 recurring meetings on your calendar, none of which will produce a decision.

The score is not money. The score is **meetings attended**. The game rewards the exact behavior that makes modern tech companies incomprehensible: saying nothing, agreeing with everything, and presenting a 47-slide deck about a shape you call "the flywheel."

---

## Controls

| Where | Input | What happens |
|---|---|---|
| Title | `Click` / `Space` / `Enter` | Clock in and start the workday |
| Invite card | `Space` or **JOIN CALL** | Accept and join the meeting |
| Invite card | **Decline** or wait 12s | Decline (−60 pts, +12 min on the clock, streak reset) |
| In a call | `Space` (or the NOD button) | Nod thoughtfully (+16 engagement, 0.42s cooldown) |
| In a call | `B` (or BUZZWORD) | Drop a buzzword (+40 pts, +6 engagement, fills a bingo chip) |
| In a call | `1` `2` `3` or click a card | Choose which deck to screen-share |
| Call debrief | `Space` / `Click` | Continue to the next invite (auto-advances after 2.6s) |
| Results | `Space` / **CLOCK IN AGAIN** | New workday |

Mouse-only works for everything except nod-mashing, which is much better on the spacebar. On the phone build every row above is also a button you can tap — keyboard bindings still work if you have one attached.

---

## How a workday works

1. **An invite lands.** A card slides in with the meeting title, host, attendee count, duration, and a tagline that explains precisely nothing. You have 12 seconds before it self-destructs.
2. **You join.** Your webcam frame appears, a 3×2 grid of attendees appears — roughly half are black tiles with initials because their cameras are off, and one of them is eating. Your **ENGAGEMENT** bar starts draining immediately.
3. **You perform.** Nodding refills engagement. Too fast and you get a warning that HR has been notified. Nodding nothing and reaching zero halves the meeting's score.
4. **You get the floor at 3.2 seconds.** Three decks appear. You have 3.7 seconds to pick one:
   - the **absurd** one (+260 points, streak intact)
   - the **cringe** one (+90 points)
   - the one that **contains actual information** (−140 points, streak destroyed, achievement unlocked)
5. **The call ends.** A debrief breaks down your score. The clock lurches forward by the meeting's length. Repeat until 5:00 PM.

**The streak** rises with every meeting you attend without declining. The multiplier follows the pattern 1, 1, 2, 2, 3, 3, 4 (capped at ×4).

**Calendar collisions** happen on 28% of calls: you are triple-booked, get +150 points immediately, and your engagement drains 50% faster. This is not a penalty, it is a personality.

---

## Scoring

Every meeting pays:

```
base   = (100 + min(attendees, 60) × 5) × (0.6 + engagement% × 0.009)
total  = round((base + deck + buzzwords) × streak multiplier)
```

with `total` halved if you let engagement hit zero.

| Action | Points |
|---|---|
| Attend a meeting | 60–600, from the base formula above |
| Absurd deck | **+260** |
| Cringe deck | +90 |
| Real numbers / audited financials / legal | **−140** and streak reset |
| Show nothing (deck timer expires) | −60 |
| Buzzword | +40 each (6 per call) |
| Full buzzword bingo | +120 bonus |
| Calendar collision | +150 |
| Decline a meeting | −60 |

A clean playthrough is 15–17 meetings. A good score is around 25,000–40,000; the ceiling is a bit above 50,000.

---

## Ranks

| Score | Rank |
|---|---|
| 45,000+ | **PIGEON BILLIONAIRE TECH BRO** |
| 30,000+ | CHIEF VIBES OFFICER |
| 19,000+ | DIRECTOR OF ALIGNMENT |
| 11,000+ | MIDDLE MANAGER (SYNC OWNER) |
| 5,000+ | INDIVIDUAL CONTRIBUTOR |
| below 5,000 | ACTUALLY WORKING (THIS WILL BE NOTED) |

---

## Achievements (11)

| Badge | How you get it |
|---|---|
| First Pointless Meeting | Attend one meeting |
| Nod Machine | Nod 40 times |
| Slide Deck Royalty | Present 5 absurd decks |
| Introduced Reality | Show a deck containing real numbers |
| Buzzword Fluent | Get all six buzzwords in a single call |
| Triple-Booked | Trigger a calendar collision |
| Streak ×5 | Five meetings without declining |
| Camera On Legend | End 5 calls with engagement above 80% |
| Boundaries (Career-Limiting) | Decline three meetings |
| Survived The Workday | Reach 5:00 PM |
| 0 Minutes of Actual Work | Reach 5:00 PM (this is not optional) |

---

## What's in it

- **32 meetings**, including *Weekly Sync To Schedule The Sync*, *All-Hands: Layoffs (Camera Mandatory)*, *1:1 To Discuss Why We Have So Many 1:1s*, *Comp Committee: The CEO's Pay* (1 attendee, quorum: 1), *Mars Colony Roadmap: Q3 Deliverables*, *Return Of The Metaverse (It Never Left)*, *Skip-Level Skip-Level Skip-Level*, and *Deep Work Block (Replaced By This)*.
- **31 decks** — 16 absurd (*AGI In Six Weeks (Slide 4 Is A Meme)*, *Turtleneck Procurement Roadmap*, *We Fired 4,000 People (Chart Is A Smiley)*, *Vibes-Based Forecasting*), 8 cringe (*My Podcast Pitch (12 Slides)*, *Nap Pod ROI Analysis*), 7 fatal (*Q4 Revenue (Actual Numbers)*, *Legal: We Are Being Sued*).
- **12 scrolling news headlines** under every call, because the founder tweeted again.
- **A permanent HUD counter reading `REAL WORK 0 MIN`** that never changes.
- Six attendee archetypes, three pigeon facial expressions, and a framed certificate on the wall reading `$0 Q3 REVENUE`.

---

## Art and audio

All artwork is drawn procedurally on a canvas at runtime — no images, no sprite sheets, no fonts to download. The pigeon is a single closed bezier silhouette (plump body, thick neck, oversized head) with cel shading, a rim light, an iridescent neck, a rotating wing-arm, blinking eyes, a beak that flaps when you nod, over-ear headphones and a boom mic.

The palette was sampled directly from the reference art in this folder (`pigeonBro.jpeg`, 1306×1204):

| Role | Hex |
|---|---|
| Sky / video background | `#7bc7f3` `#5fabe2` `#4186be` |
| Pigeon body | `#cfdbdf` `#bab7b2` |
| Warm greys, desk, floor | `#9c9188` `#8a7969` `#5f4c40` |
| Turtleneck, outlines | `#292523` `#101113` |

Sound is a tiny WebAudio synth: an invite chime, a nod blip, a deck fanfare, a decline buzz, and a sad tone when you show real numbers.

---

## Technical notes

- **Two files, ~68 KB each, zero dependencies.** No frameworks, no CDN, no build. The phone build is the same codebase with a portrait stage, a re-stacked CSS layout and touch input.
- Canvas 2D for the character, room and effects; plain DOM/CSS for panels, buttons and HUD.
- Device-pixel-ratio aware (capped at 2×) with CSS transform scaling to any viewport.
- Fixed timestep clamp (max 50 ms per frame) so tab-switching can't skip a call; the game pauses when the tab is hidden.
- No storage, no cookies, no network, no telemetry. Refreshing loses your run.
- Measured at **60 fps** in both the office and the call scene in headless Chromium.
- A debug handle is exposed as `window.__PB` (game state plus the flow functions) for tinkering in the console.

### Verification

Driven end-to-end with Playwright against real Chromium: full 17-meeting workdays complete without a single page or console error, all three play styles (optimal, random, decline-everything) reach the results screen with correct stats, every panel and button sits inside the 1280×720 stage with no overflow, and no score or clock value can become `NaN`.

---

## Packaging as a desktop .exe

The game is already a self-contained page, so packaging is a wrapper, not a port.

**Electron** (fastest — this folder's machine already has `electron` and `electron-builder`):

```js
// main.js
const { app, BrowserWindow } = require('electron');
app.whenReady().then(() => {
  const win = new BrowserWindow({ width: 1300, height: 760, autoHideMenuBar: true,
    backgroundColor: '#120d0a', useContentSize: true });
  win.loadFile('pigeon_bro_1.html');
});
```

```bash
npm init -y && npm i -D electron electron-builder
npx electron .                 # run it
npx electron-builder --win     # produces a portable .exe in dist/
```

**Tauri** if you want a ~5 MB binary instead of ~150 MB: same HTML, `tauri.conf.json` pointing `build.frontendDist` at this folder, `tauri build` for `.msi`/`.exe`.

---

## A note on the satire

Everything here is a joke about patterns, not people. Any resemblance to a specific billionaire you have tweeted about is coincidental, and — legally speaking — hilarious.

*Made with a pigeon, a calendar, and no decisions.*
