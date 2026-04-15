# TypeForge

A personal touch typing training system built as a single self-contained HTML file. No installation, no account, no server — just open it in a browser and train.

## Philosophy

**Accuracy first, speed second.**

At typical beginner speeds the bottleneck is not finger movement — it is hesitation from uncertain muscle memory. TypeForge drills accuracy on a small set of patterns until they become automatic, then expands the vocabulary, then trains speed on what is already solid.

## Stage System

Progress is measured in **Stages**, not abstract points. Each stage maps to a real typing milestone and unlocks automatically when the user passes a **Stage Gate** — a 60-second test requiring both a minimum WPM and minimum accuracy simultaneously.

| Stage | Name | Gate |
|-------|------|------|
| 0 | Foundation | Home row only — no gate |
| 1 | Apprentice | 40 WPM · 92% accuracy |
| 2 | Builder | 55 WPM · 94% accuracy |
| 3 | Journeyman | 70 WPM · 95% accuracy |
| 4 | Craftsman | 85 WPM · 96% accuracy |
| 5 | Expert | 100 WPM · 97% accuracy |
| 6 | Master | 110+ WPM · 98% accuracy |

Stages cannot be skipped. Each one builds the muscle memory patterns that the next stage accelerates.

## Features

- Single HTML file — zero setup, runs offline
- Local storage for all progress data
- Stage-gated progression system
- Multiple training modes: standard drills, Speed Burst, Rhythm Typing, Flow Typing, Speed Sprint
- Problem Key Drill — automatically targets your weakest keys
- Custom text import at Stage 6
- Real-time WPM and accuracy feedback

## Getting Started

```bash
git clone https://github.com/Desstter/typeforge.git
cd typeforge
open typeforge.html
```

Or just download `typeforge.html` and open it directly.

## Tech Stack

- HTML5 / CSS3
- Vanilla JavaScript
- Web Storage API (localStorage)
- No dependencies, no build step

## Design Principles

- No social features, no leaderboards — solo training only
- Data stays entirely on your machine
- Interface shows only what serves the current training session
- Based on motor learning science: spaced repetition and deliberate practice with error-correction loops

## License

MIT
