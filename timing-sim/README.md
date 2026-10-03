# PTP/SyncE Network-Wide Timing Simulator

Simulate a full PTP/SyncE timing chain **over time** — not just a static
budget. Draw a chain of grandmaster, boundary, transparent, and slave clocks,
set per-hop asymmetry and noise, then watch hours of PTP time error play out:
PI servo wander, holdover drift, and ITU-T G.8273.2 Class A–D pass/fail for
every clock.

**Live version:**
[allaboutitinfrastructure.com/tools/timing-sim/](https://allaboutitinfrastructure.com/tools/timing-sim/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

> **Simplified planning models — not a substitute for lab validation** against
> real hardware and ITU-T test setups. The simplifications are listed below
> and on the page itself.

## How to use

1. **Build the chain** — click to add nodes (grandmaster, boundary clock,
   transparent clock, slave), connect them with fiber spans. Presets included
   for common chain shapes.
2. **Configure each node** — clock type, PI servo gains (sane defaults),
   oscillator stability (ppm) for holdover, per-span asymmetry (ns) and PDV
   noise profile (none / quiet / typical / noisy).
3. **Run the simulation** — discrete-time, 1 s timestep, one two-way PTP
   exchange per step, over as many simulated hours as you want. Seeded PRNG,
   so every run is reproducible.
4. **Read the results** — time-error-vs-time chart, max|TE| / max|TEL| table
   per node, G.8273.2 class matrix (A/B/C: max|TE| ≤ 100/70/30 ns; D: max|TEL|
   ≤ 5 ns after a 0.1 Hz low-pass — the tool applies a digital LPF before
   checking D), hops ranked by noise contribution, and a GPS-loss holdover
   mode that shows drift on local oscillators.

## The models, in brief (and their honest limits)

- **PI servo per slave/boundary clock**, driven by the two-way offset
  measurement against its upstream master. The integrator is preloaded to
  cancel the *configured* static ppm — the model starts frequency-locked and
  only acquires phase, asymmetry bias, and noise. A real cold-starting servo
  would show a longer pull-in transient.
- **Asymmetry bias**: every span's forward/reverse delay difference adds
  asym/2 to the offset measurement — the error PTP cannot see. This is the
  dominant term in most real deployments.
- **Clock noise** is a *filtered-noise approximation* of power-law clock
  noise: white Gaussian noise through a first-order low-pass (τ ≈ 30 s) plus
  a random-walk component. Qualitatively right; not a calibrated
  oscillator model.
- **Holdover**: after the configured GPS-loss time, all exchanges stop and
  every clock free-runs on its local oscillator (ppm) plus wander.
- Transparent clocks are pass-through (no servo, no phase state).

## Validated

Against the shipped simulation core (seeded, deterministic):

- Zero-noise 3-node chain → max|TE| = **0 ns** on every clock
- Single hop, 100 ns asymmetry → steady-state offset **−50.00 ns** (= −asym/2)
- 1 ppm oscillator, 1 h holdover → drift **3.601 ms** (≈ 3.6 ms expected)
- Identical seed + config run twice → **bit-identical** results
