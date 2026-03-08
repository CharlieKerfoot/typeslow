# Evaluation Criteria

## What We're Measuring

The core mechanic has three sub-components. Each must pass independently.

---

## Pass Criteria

### 1. Bigram Detection Accuracy (MUST PASS)
- **Test:** After calibration, the system identifies the user's 20 slowest bigrams.
- **Pass:** At least 15 of the 20 identified bigrams have a median transition time ≥1.5x the user's overall median bigram time. (i.e., the system is actually finding slow bigrams, not noise)
- **How to verify:** The results screen shows each targeted bigram's calibration time vs. overall median. Count how many are ≥1.5x.

### 2. Text Generation Oversampling (MUST PASS)
- **Test:** The generated training text contains the targeted bigrams at a significantly higher rate than natural English.
- **Pass:** The 20 targeted bigrams appear at ≥3x their natural English frequency in the generated training passages. (Natural bigram frequencies are computed from the calibration text as a baseline.)
- **How to verify:** The results screen shows targeted bigram density in training text vs. calibration text.

### 3. Measurable Bigram Improvement (PRIMARY METRIC)
- **Test:** After the training phase, the user's median transition time on the 20 targeted bigrams decreases.
- **Pass:** Median transition time on targeted bigrams decreases by ≥10% from Phase 1 to Phase 3, AND this improvement is at least 5 percentage points greater than the improvement on non-targeted bigrams (to control for general warm-up effects).
- **How to verify:** The results screen shows before/after median times for targeted vs. non-targeted bigrams with percentage changes.

### 4. Qualitative Usability (SHOULD PASS)
- **Test:** Run with 5 people. Ask: "Did the practice text feel harder than the calibration text?" and "Were you frustrated by not seeing your speed?"
- **Pass:** ≥3 of 5 say the practice text felt harder (confirms targeting). ≤2 of 5 say the hidden metrics were frustrating enough to want to quit.

---

## Fail Criteria

- If bigram detection finds fewer than 15/20 genuinely slow bigrams → the timing analysis is too noisy; need better filtering.
- If generated text doesn't hit 3x oversampling → the text generation algorithm is too constrained; need a better approach.
- If targeted bigram improvement is <10% OR not at least 5pp above non-targeted improvement → the core mechanic doesn't work; the adaptive targeting doesn't produce differential improvement.
- If 3+ of 5 users want to quit due to hidden metrics → the "hide the score" design needs rethinking.

---

## Decision

- **All 3 quantitative criteria pass:** Proceed to 2-week protocol design.
- **Criteria 1 & 2 pass but 3 fails:** The targeting works but one session isn't enough. Consider a 3-day mini-study.
- **Criterion 1 or 2 fails:** Fundamental mechanic is broken. Debug before proceeding.
