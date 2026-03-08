# Experiment: RetroType Bigram Trainer

## Hypothesis

Keystroke-level timing analysis can identify a user's slowest bigram transitions, and practice text that oversamples those bigrams (with hidden real-time metrics) will produce measurably faster typing on those specific bigrams within a single session.

## What This Tests

This experiment tests ONLY the core mechanic: can we (1) accurately identify a user's slowest bigrams from keystroke timing, (2) generate readable practice text that oversamples those bigrams, and (3) demonstrate measurable improvement on those specific bigrams within one 10-minute session?

We are NOT testing retention, long-term improvement, or the full 2-week protocol. We're testing whether the adaptive targeting loop works at all.

## How It Works

1. **Calibration Phase (Phase 1):** User types 3 passages of standard English text. Keystroke-level timing captures every key-down event and computes bigram transition times.
2. **Analysis:** The system ranks all observed bigrams by median transition time and selects the 20 slowest.
3. **Training Phase (Phase 2):** The system generates 5 passages that oversample the user's slowest bigrams. NO speed metrics are shown during typing — only a progress bar.
4. **Retest Phase (Phase 3):** User types 3 more standard passages (same difficulty as Phase 1 but different text). Bigram times are re-measured.
5. **Results:** A before/after comparison of the 20 targeted bigrams is displayed, along with overall WPM.

## Setup

```bash
# No build step needed. Just serve the HTML file:
python -m http.server 8000
# Then open http://localhost:8000/index.html in your browser
```

## Data Collection

All data stays in the browser (localStorage). At the end of a session, the user can optionally copy a JSON blob of anonymized results to clipboard for aggregation.

## Architecture

Single HTML file with embedded CSS and JavaScript. No dependencies, no server, no frameworks. Keystroke timing uses `performance.now()` for sub-millisecond precision.