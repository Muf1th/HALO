# Halo

A recovery, strain and sleep tracker with a dark liquid-glass design. You enter a few numbers each morning (from your phone's health app or any watch), and Halo works out:

- **Recovery** (0–100%) from HRV, resting heart rate and sleep, compared with your own 14-day norm
- **Strain** (0–21) from your activities, using average heart rate when you have it and how hard it felt when you don't
- **Sleep need** for tonight, adjusted for today's strain and any sleep debt, with bedtimes for 100%, 85% and 70% of that need
- **Health monitor**: HRV, resting heart rate, respiratory rate, blood oxygen and skin temperature against your norm
- **Sleep consistency** from your bed and wake times
- **Journal insights**: how habits like alcohol or late caffeine shift your recovery
- **Weekly report** comparing the last 7 days with the 7 before

It is one self-contained file, `index.html`, with no build step and no dependencies beyond one Google Font.

## Running it

- Open `index.html` in a browser, or
- Turn on GitHub Pages for this repo (Settings → Pages → deploy from `main`, root) and open the link on your phone. Add it to your home screen for an app-like feel.

## Where your data lives

- **Inside Claude** (as a claude.ai artifact): entries are saved to your account and only you can see them.
- **Anywhere else** (GitHub Pages, a local file): entries are saved in that browser's local storage, on that device only. Clearing site data erases them.

## How the scores work

These are simplified formulas, not WHOOP's proprietary ones.

| Score | Formula |
| --- | --- |
| Recovery | 50% HRV vs norm (60–140% mapped to 0–100) + 20% resting HR vs norm (±15%) + 30% sleep performance |
| Sleep performance | time asleep ÷ sleep need, capped at 100% |
| Sleep need | baseline (default 8h) + 0.06h per strain point above 10 + half of last night's shortfall (max 1.5h) |
| Strain | 21 × (1 − e^(−load/120)), where load = 30 for daily living + each activity's load |
| Activity load (with HR) | minutes × HRR × 0.64 × e^(1.92 × HRR) × 1.15, where HRR = (avg HR − resting HR) ÷ (max HR − resting HR) |
| Activity load (effort) | minutes × (effort ÷ 10)² × 4 |
| Max HR | 208 − 0.7 × age |

Scores are for training guidance only and are not medical advice.
