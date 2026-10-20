# PTP Holdover Planner

GPS just died — how long until your clock drifts outside its limit? Enter your oscillator's frequency offset and ageing (or pick a preset: TCXO, OCXO, high-holdover OCXO module, chip-scale atomic, rubidium) and get the time-error growth curve, the exact crossing time for the ±100 ns, ±1 µs, ±1.5 µs and ±10 µs limits plus your own custom limit, and a reverse mode that names the oscillator class you actually need for a target outage.

**Live version:**
[allaboutitinfrastructure.com/tools/ptp-holdover/](https://allaboutitinfrastructure.com/tools/ptp-holdover/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Start from the standard OCXO preset: offset 0.1 ppb, no ageing. Over 24 hours it drifts 8.64 µs, and it crosses the ±1.5 µs telecom limit at exactly 15,000 seconds (4.17 hours).
2. Pick another preset or type your own offset (ppb), ageing (ppb/day) and starting error — the curve, the end-of-outage error and the crossing table update live.
3. Use the reverse mode ("What oscillator do I need?"): give it a target duration and limit and it computes the maximum survivable offset, then names the cheapest preset class that stays inside — honestly. The high-holdover OCXO module preset computes to 1,503 ns over 24 hours, so against a 1,500 ns target it is flagged "at the line", not a pass.

## The model

Time error grows as TE(t) = TE0 + y0·t + ½·D·t² — a constant frequency offset accumulates error linearly, and ageing (the frequency itself drifting) makes it accelerate quadratically. Temperature is NOT modelled: the tool assumes constant temperature, and a temperature swing adds error on top, so the real crossing comes sooner, never later. Preset figures are anchored to published ranges checked in October 2026 (good OCXOs roughly 1–10 µs over 24 hours, rubidium roughly 100–500 ns over 24 hours; the high-holdover module preset follows the IQD IQCM-300's published 1.5 µs-over-24-hours adaptive-algorithm specification).

Honest note: explainers and vendor pages publish holdover rules of thumb, but no free web tool was found (October 2026 market check) that runs your own offset, ageing and limit numbers. The network-side questions live in the companion tools: the PTP timing budget calculator (error budget while locked) and the PTP/SyncE timing simulator (multi-hop network behaviour).
