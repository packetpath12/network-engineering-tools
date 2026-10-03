# ECMP Hash Polarization Visualizer

ECMP spreads flows across equal-cost paths by hashing each packet's 5-tuple —
but when every switch in a Clos fabric runs the same hash with the same seed,
the choices stop being independent and traffic polarizes onto a few hot paths.
Run the simulation and watch it happen, then flip the seed mode and watch it
heal.

**Live version:**
[allaboutitinfrastructure.com/tools/ecmp-hash/](https://allaboutitinfrastructure.com/tools/ecmp-hash/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Set **spines (S)**, **leaves (L)**, and **flows (N)** for your fabric.
2. Pick **Identical seed on every switch** (the failure mode) or **Per-switch
   varied seeds** (the fix), then **Run simulation**.
3. Read the **polarization ratio** (max ÷ mean cell load): under ~1.5× is a
   healthy fabric, over ~2× is polarized.
4. The **stage-2 bar chart** shows flows per spine→leaf link against the
   perfectly-even share; the **joint heatmap** shows the full stage-1 ×
   stage-2 distribution — polarization lights up a diagonal while the rest of
   the grid idles.

## The logic, in brief

Each of N random 5-tuples (src/dst IP, src/dst port, protocol) is hashed with
seeded FNV-1a finished with the MurmurHash3 `fmix32` avalanche. Stage 1
(leaf→spine) takes `hash % S`; stage 2 (spine→leaf) either reuses the same hash
(identical-seed mode — correlated) or hashes again with an independent seed
(varied-seed mode — decorrelated).

One honest implementation note, also stated on the page: raw FNV-1a's low bits
— the bits the modulo reads — barely respond to a change in the initial seed,
so without the `fmix32` finishing step the "varied seeds" mode could not
decorrelate. Real switch ASICs use CRC- or Toeplitz-family hashes with proper
avalanche for the same reason.

## Validated

- 20,000 flows / 8×8 fabric, varied seeds → polarization ratio **< 1.5**
- Same setup, identical seeds → polarization ratio **> 2.0** (traffic on the diagonal)
- Total flows assigned **= 20,000** in both modes
