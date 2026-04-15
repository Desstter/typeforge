# TypeForge — Personal Touch Typing Training System
### Design Document v1.0

---

## 1. Overall Concept

**TypeForge** is a personal, web-based touch typing training system built around one core philosophy: **accuracy first, speed second**. It is designed for a single user working alone, with no social or competitive features. The system is a single HTML file that runs in any browser, stores all data locally, and requires zero setup or installation.

The design draws from three disciplines:
- **Motor learning science** — spaced repetition, deliberate practice, and error-correction loops
- **Game design** — visible progress, milestone unlocks, and a satisfying feedback loop
- **UX minimalism** — nothing on screen that doesn't serve the training session

The central training philosophy is:

> Type slower than you think you need to. Then get faster.

At 40 WPM, the primary bottleneck is not finger speed — it is hesitation caused by uncertain muscle memory. TypeForge resolves this by drilling accuracy on a small set of patterns until they become automatic, then expanding the vocabulary of patterns, then training speed on what is already automatic.

---

## 2. Learning Progression

### The Stage System

Progress is measured in **Stages**, not points or abstract XP. Each Stage maps directly to a real-world typing milestone. Stages are unlocked automatically when the user passes a **Stage Gate**: a short test exercise requiring both a minimum WPM and a minimum accuracy.

```
Stage 0 — Foundation      (Home row only)
Stage 1 — Apprentice      40 WPM  |  92% accuracy
Stage 2 — Builder         55 WPM  |  94% accuracy
Stage 3 — Journeyman      70 WPM  |  95% accuracy
Stage 4 — Craftsman       85 WPM  |  96% accuracy
Stage 5 — Expert         100 WPM  |  97% accuracy
Stage 6 — Master         110+ WPM |  98% accuracy
```

The user starts at Stage 0 regardless of current speed, because the Foundation stage resets bad habits and establishes correct finger positioning before speed training begins.

### Stage Gating Rules

A Stage Gate is triggered when the user completes any standard exercise and the trailing 3-exercise average meets the threshold. The gate is a 60-second test on a fixed text at that stage's word difficulty. Both conditions (WPM **and** accuracy) must be met simultaneously.

**You cannot skip stages.** Each stage builds the muscle memory patterns that the next stage accelerates.

### What Unlocks with Each Stage

| Stage | Unlocks |
|-------|---------|
| 0 | Home row drills, basic bigrams |
| 1 | All letter drills, common word list (top 200), Speed Burst mode |
| 2 | Rhythm Typing mode, trigrams, top 500 words |
| 3 | Flow Typing mode, real sentence practice, top 1000 words |
| 4 | Full text passages, advanced bigrams, Problem Key Drill |
| 5 | Speed Sprint mode, literature excerpts |
| 6 | Custom text import, max difficulty settings |

---

## 3. Training Modes

There are seven distinct training modes. Each serves a specific purpose in the progression from 40 WPM to 100+ WPM.

---

### Mode 1 — Home Row Foundation

**Purpose:** Reset posture and finger placement. Eliminate wrong-finger habits before they compound at speed.

**How it works:**

The exercise area shows only the home row: `A S D F G H J K L ;`. Letters fall or appear in sequence, and the user types them without looking at the keyboard. No time pressure. A visual keyboard is always on screen showing which finger should press which key, color-coded by hand and finger.

Exercises are built from:
- Pure home row sequences: `asdf jkl; fdsa ;lkj`
- Simple alternating patterns: `aj sk dl f;`
- Short "finger ladder" sequences that train each finger individually

**Accuracy rule:** Any error causes the current sequence to restart. There is no penalty counter — just a restart. This builds the habit of stopping rather than pushing through errors.

**Graduates to Stage 1 when:** The user completes 3 consecutive home row exercises at 100% accuracy, regardless of speed.

---

### Mode 2 — Letter Pattern Drill

**Purpose:** Build muscle memory for the most common English letter combinations before full words are introduced.

**Structure:**

Exercises are built around **bigrams** and **trigrams** — pairs and triplets of letters that appear most frequently in English text. The system trains these from the most common downward.

**Top bigrams trained (by frequency in English):**
`th`, `he`, `in`, `er`, `an`, `re`, `on`, `en`, `at`, `es`, `ed`, `it`, `ou`, `to`, `ha`, `ng`, `st`, `nd`, `or`, `is`

**Top trigrams trained:**
`the`, `and`, `ing`, `ion`, `ent`, `ati`, `for`, `her`, `ter`, `hat`

Each exercise presents a pattern repeated with variations:
```
the then there they their
and hand stand band grand
ing ring bring thing
```

**Accuracy gate:** The user cannot advance to the next pattern group until they complete the current one at 97%+ accuracy three times in a row. The accuracy threshold is deliberately high here because this is muscle memory formation — the whole point is to engrave the pattern correctly.

**Progression within the mode:** Patterns are introduced in frequency order. The user always trains on the most common patterns they haven't yet mastered.

---

### Mode 3 — Word Training

**Purpose:** Move from patterns to real words. Train common English vocabulary until words are typed as single fluid motions rather than letter-by-letter.

**Word Lists (by Stage):**

The word lists are sourced from English word frequency data. Words are not random — they are selected specifically because they cover the highest-frequency letter combinations.

- Stage 1: Top 200 most common English words
- Stage 2: Top 500 words
- Stage 3: Top 1000 words
- Stage 4+: Top 3000 words + domain words (technical, everyday, etc.)

**Exercise format:**

Words are displayed one at a time or in short groups of 5. The user types them. After each word:
- Green flash = correct
- Red highlight = error, the word is added to the **Problem Pool** (see Analytics)

Words from the Problem Pool appear 3× more frequently than normal words until they are typed correctly 5 times in a row, at which point they are "cleared" from the pool.

**Speed target display:** A subtle WPM estimate is shown live. No pressure, just awareness.

---

### Mode 4 — Speed Burst

**Purpose:** Train raw finger speed in short intense bursts without the pressure of maintaining it for a long session.

**How it works:**

The user sees a single word or short phrase (5–8 characters). They type it as fast as possible. Then another appears immediately. This continues for 30 seconds.

WPM for bursts is measured and displayed after each session. The highest ever burst WPM is tracked separately as "Burst Record."

**Why bursts work:** The nervous system learns maximum speed from short maximum-effort attempts, not from long moderate-effort sessions. Burst training teaches the hands what fast feels like, and that feeling gradually becomes the new normal.

**Rule:** If accuracy drops below 85% during a burst session, the session ends with a "Slow down" message and restarts. This prevents the user from training bad sloppy habits at speed.

---

### Mode 5 — Rhythm Typing

**Purpose:** Eliminate the uneven, hesitant rhythm of an intermediate typist and replace it with a steady, consistent keystroke cadence.

**How it works:**

A soft metronome beat plays in the background. The user must type each character on or near a beat. The beat speed is set to match a slightly slower pace than the user's average, then gradually increases.

The system uses the browser's Web Audio API for the metronome sound. No external files required.

The screen shows the text and a simple visual pulse — a small circle that expands on each beat.

**The key insight:** Most typists at 40–70 WPM are not slow because their fingers are slow. They are slow because they have irregular pauses — they type some words fast and some words very slowly. Rhythm training eliminates the slow patches.

**BPM progression:**

The starting BPM is set automatically based on the user's average WPM from recent sessions. BPM increases by 5 after each successful rhythm session (defined as ≥90% of keystrokes within ±20ms of a beat).

---

### Mode 6 — Flow Typing

**Purpose:** Practice typing full English sentences and paragraphs at target speed with natural language patterns.

**Text sources:**

Stage 3+: Common English sentences (crafted for typing coverage)
Stage 4+: Short passages from classic English literature
Stage 6+: User-imported custom text

**How it works:**

Text is displayed in a paragraph format, not word-by-word. The cursor advances as the user types. Errors are highlighted in red but the user **can continue** (unlike pattern drills). This mode is about flow, not perfection — though accuracy is still measured.

At the end of each passage, the user sees:
- WPM for the passage
- Accuracy %
- A list of every mistyped word
- A heatmap of error positions within the text

**The accuracy rule shifts here:** In Flow mode, the goal is to keep errors below 3% while maintaining target speed. This simulates real-world typing where the user must produce correct output quickly.

---

### Mode 7 — Problem Key Drill

**Purpose:** Identify and specifically destroy the user's weakest individual keys and combinations.

**How it works:**

The analytics system continuously tracks which keys are mistyped most often and which key transitions (from key A to key B) have the highest error rate. Problem Key Drill uses this data to generate targeted exercises.

If the user frequently misses `b`, the drill generates:
```
be by but back because before been between
```

If the transition `er` is a common error:
```
her there were every never other
```

The drill runs for 3 minutes. After the drill, the analytics update to show whether those keys improved.

**This mode is available from Stage 4** because the user needs enough typing history for the analytics to identify meaningful patterns.

---

## 4. Analytics and Personal Record System

The analytics system is the backbone of personal improvement. It is always running in the background during every exercise. All data is stored in `localStorage` in the browser — no server, no account, no internet required.

---

### Live Session Stats

Displayed during every exercise in a clean header bar:

```
  WPM: 67      Accuracy: 94.2%      Errors: 3      Time: 01:23
```

These update in real time. WPM is calculated using the standard formula: `(characters typed / 5) / minutes elapsed`.

---

### Session Summary

After every exercise, a summary card appears before returning to the menu:

```
SESSION COMPLETE
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  WPM           71         ↑ +4 from last session
  Accuracy      95.3%      ↑ +1.1%
  Duration      02:15
  Errors        7

  Problematic keys:  b  (4×)    y  (2×)    p  (1×)

  Personal Best:     ★ New best WPM!  (was 68)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### Personal Records Panel

A dedicated "Records" screen, accessible from the main menu, showing:

```
PERSONAL RECORDS
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  SPEED
  Best WPM (Flow)        71 wpm     Mar 14, 2026
  Best WPM (Burst)       89 wpm     Mar 12, 2026
  Best WPM (Rhythm)      74 wpm     Mar 13, 2026

  ACCURACY
  Best Accuracy          99.1%      Mar 10, 2026
  Longest Perfect Streak 47 chars   Mar 11, 2026
  Best Error-Free Run    Full pass  Mar 9, 2026

  STREAKS
  Most Sessions in a Row    6 days
  Current Stage             3 — Journeyman

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Records are never deleted. A small star icon (★) appears next to the stat when a new personal best is set during a session.

---

### Progress Chart

A simple line graph (drawn on an HTML `<canvas>` element) shows WPM over the last 20–50 sessions. Two lines: one for accuracy (right axis), one for WPM (left axis). The user can see their trend at a glance.

---

### Key Heatmap

A visual keyboard layout where each key is shaded from green (rarely missed) to red (frequently missed). Updated after every session. Lets the user see at a glance which fingers/regions need work.

---

### Problem Pool Dashboard

A small table showing the user's current "problem words" — the 10 words from Word Training mode that have been missed most recently. Shown on the Stats screen and cleared when a word is typed correctly 5 times in a row.

```
CURRENT PROBLEM WORDS
  because   ████████  8 recent errors
  through   ██████    6 errors
  between   █████     5 errors
  should    ████      4 errors
  ...
```

---

### Data Storage Structure

All data is stored as a JSON object in `localStorage` under the key `typeforge_data`. Structure:

```json
{
  "stage": 3,
  "sessions": [
    {
      "date": "2026-03-14",
      "mode": "flow",
      "wpm": 71,
      "accuracy": 95.3,
      "errors": 7,
      "duration": 135,
      "errorKeys": {"b": 4, "y": 2, "p": 1}
    }
  ],
  "records": {
    "bestWPM": 71,
    "bestAccuracy": 99.1,
    "bestBurstWPM": 89,
    "longestStreak": 47
  },
  "problemPool": ["because", "through", "between"],
  "keyErrorCounts": {"b": 42, "y": 31, "p": 18}
}
```

This data structure is compact, easy to back up (the user can copy-paste it), and requires no database.

---

## 5. UI Structure

The interface is designed around a single principle: **nothing on screen except what is needed for the current action.**

---

### Screen Map

```
[ Main Menu ]
    │
    ├─ [ Train ]
    │       ├─ Mode Select
    │       └─ [ Exercise Screen ]
    │               └─ [ Session Summary ] → back to Mode Select
    │
    ├─ [ Records ]
    │       ├─ Personal Bests
    │       ├─ Progress Chart
    │       └─ Key Heatmap
    │
    ├─ [ Stage Progress ]
    │       └─ Stage overview + Gate Test trigger
    │
    └─ [ Settings ]
            ├─ Font size
            ├─ Sound on/off
            ├─ Metronome BPM adjustment
            └─ Export / Import data (JSON)
```

---

### Main Menu

Clean, dark background. Large stage badge at top ("Stage 3 — Journeyman"). Five large buttons: Train, Records, Stage Progress, Settings, and a small "Today's summary" strip at the bottom showing the day's session count and average WPM.

---

### Exercise Screen Layout

```
┌─────────────────────────────────────────────────────────────────┐
│  WPM: 67   Accuracy: 94%   Errors: 3   [■■■■■░░░░░]  01:23      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   the quick brown fox jumps over the lazy dog                  │
│   the quick brown fox ju|ms over the lazy dog                  │
│       ↑ typed (green)     ↑ cursor   ↑ upcoming (gray)         │
│                                                                 │
│   [x - error shown in red with soft red background]            │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                  VISUAL KEYBOARD (optional)                     │
│  [A][S][D][F][G] [H][J][K][L][;]  — finger colors shown       │
└─────────────────────────────────────────────────────────────────┘
```

**Text display rules:**
- Current character to type: bright white, cursor underline
- Correctly typed characters: medium gray (moved behind, not the focus)
- Error character: red background, red text — stays visible until corrected
- Upcoming characters: dim gray

The visual keyboard can be toggled on/off with `Tab`. When shown, the key that should be pressed next is highlighted, and the suggested finger is shown by color.

**Finger color coding:**
- Left pinky = dark purple
- Left ring = blue
- Left middle = teal
- Left index = green
- Right index = yellow-green
- Right middle = orange
- Right ring = red-orange
- Right pinky = red

---

### Records Screen Layout

Divided into three sections: **Personal Bests** (card grid), **Progress Chart** (canvas), **Key Heatmap** (canvas keyboard). All on one scrollable page.

---

### Stage Progress Screen

A horizontal "road" graphic showing all 7 stages as stops on a path. Current stage is highlighted. Completed stages show a checkmark. The next stage shows the requirements to unlock it and a "Take Stage Gate Test" button when the user's recent average is close.

---

## 6. Simplest Architecture to Implement Quickly

### Technology Stack

The entire system is **a single HTML file**. No framework, no build step, no server, no npm, no dependencies.

```
typeforge.html
```

That is the entire file structure.

**Inside the file:**
- HTML structure (the five screens)
- CSS (embedded in `<style>` — dark theme, ~200 lines)
- JavaScript (embedded in `<script>` — all logic, ~800–1200 lines)
- Word lists and exercise text (embedded as JS arrays, ~300 lines)

**Browser APIs used:**
- `localStorage` — all data persistence
- `<canvas>` — progress chart and key heatmap
- `Web Audio API` — metronome click for Rhythm mode (one line of audio synthesis, no files)
- Standard DOM events — keydown listener for all typing input

### Implementation Order (Recommended)

Build in this order to have a functional system as quickly as possible:

**Phase 1 — Core loop (Day 1–2)**
1. Single screen with a text exercise
2. Keydown listener that compares input to expected character
3. Live WPM and accuracy counters
4. Session summary screen
5. localStorage save of session data

**Phase 2 — Modes (Day 3–4)**
1. Word Training mode (uses a hardcoded array of the top 200 words)
2. Flow Typing mode (uses a hardcoded array of sentences)
3. Mode select screen

**Phase 3 — Progression (Day 5–6)**
1. Stage system with localStorage-saved stage
2. Stage Gate test trigger
3. Stage Progress screen

**Phase 4 — Analytics (Day 7–8)**
1. Key error tracking
2. Records screen with personal bests
3. Progress chart (canvas line graph)
4. Key heatmap (canvas keyboard)

**Phase 5 — Polish (Day 9–10)**
1. Visual keyboard with finger colors
2. Rhythm mode with Web Audio metronome
3. Speed Burst mode
4. Problem Key Drill (uses accumulated error data)

**Estimated total build time for a competent web developer: 15–25 hours.**

The system intentionally uses zero external libraries or CDN resources. It works offline. It can be emailed to yourself, stored on a USB drive, or opened from any folder.

---

## 7. Optional Improvements for Later Versions

These are not in scope for the initial build but would meaningfully improve the system without compromising its simplicity.

### Tier 1 — High Value, Low Effort

**Custom text import**
Allow the user to paste any text and practice on it. Adds 20 lines of JS. Available from Stage 6.

**Session notes**
A small text box after each session for the user to type a 1-line note ("felt tired," "new keyboard," etc.). Stored with session data. Helps interpret the progress chart.

**Dark/light theme toggle**
A single CSS class swap. Useful for different lighting environments.

**Keyboard layout support**
Add a Dvorak or Colemak mode that remaps the finger guidance without changing the words. Store layout preference in settings.

### Tier 2 — Medium Value, Medium Effort

**Sound effects on keystrokes**
Satisfying key click sounds using the Web Audio API. Research shows mild auditory feedback slightly improves rhythm consistency.

**Personal word timing data**
Track not just which words are mistyped but how long each word takes to type. Surface the 10 "slowest words" as a training target. Adds ~50 lines of JS.

**Spaced repetition on problem words**
Instead of a simple Problem Pool, implement a basic SR algorithm (similar to Anki's algorithm) to schedule problem word review at optimal intervals.

**Text difficulty scoring**
Rate each exercise text by average word length and bigram complexity. Display as a 1–5 difficulty star rating so the user can calibrate.

### Tier 3 — Lower Priority, Higher Effort

**PDF or CSV export of session history**
Let the user export all their data as a table for review or backup. Useful after long periods of training.

**Configurable Stage thresholds**
Allow the user to adjust stage WPM and accuracy requirements if the defaults feel too easy or too hard.

**Passage library browser**
A simple searchable list of all available flow typing texts, showing which have been completed and the user's best score on each.

---

## Summary of Key Design Decisions

**Why single HTML file?** Because the system is for personal use. Zero setup friction means the user actually opens and uses it. Every additional step — installing npm, running a server, creating an account — reduces the chance the system gets used daily.

**Why accuracy gates before speed?** Motor learning research consistently shows that practicing incorrect movements builds incorrect automaticity. Once a wrong pattern is automatic, it takes far longer to unlearn than to learn correctly from the start. The accuracy-first design is not conservative — it is the fastest route to 100 WPM.

**Why no social features?** The user's goal is personal performance improvement, not competitive ranking. Social systems introduce extrinsic motivation that can interfere with the intrinsic satisfaction of personal progress. The records system provides all the motivation needed.

**Why not use an existing tool like Monkeytype or Keybr?** Existing tools are general-purpose and optimized for engagement across many user types. TypeForge is optimized for one specific user's journey from 40 to 100 WPM, with a deliberate learning progression rather than free-form practice.

---

*TypeForge Design Document v1.0 — March 2026*
