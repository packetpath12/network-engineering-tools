# PTP Timing Budget Calculator (IEEE 1588)

How much time error does your IEEE 1588 timing chain accumulate? Enter the
boundary-clock count, per-node time error, timestamp granularity, and link
asymmetry — get worst-case and RMS end-to-end time error checked against real
budgets: 5G fronthaul, MiFID II, and power-utility timing.

**Live version:**
[allaboutitinfrastructure.com/tools/ptp-budget/](https://allaboutitinfrastructure.com/tools/ptp-budget/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. **Boundary clocks (N)** — how many boundary clocks sit in series between
   grandmaster and end application.
2. **Per-node max time error (TE_max)** — the per-node allocation, e.g. from
   the G.8273.2 clock classes (~100 ns Class A down to ~5 ns Class D).
3. **Timestamp granularity** — the node's timestamping step; it folds straight
   into that node's error (a node that timestamps in 8 ns steps cannot resolve
   time more precisely than its grid).
4. **Link asymmetry per hop** — the forward/reverse path delay difference that
   PTP's delay measurement cannot see.
5. **Target budget preset** — 5G fronthaul (1,000 ns), MiFID II (100,000 ns),
   power utility (1,000 ns), or a custom number.

The page reports worst-case and RMS totals, a pass/fail verdict with margin or
overage, the full input breakdown, and a per-hop running-worst-case table.

## The math, in brief

- **Worst case** (the number you certify against): every node error maxes out
  simultaneously with the same sign, and the fixed-sign asymmetry bias adds at
  every hop — `Σ (TE_max + granularity + asymmetry)`.
- **RMS** (where a healthy chain actually lives): node errors are treated as
  independent random variables combining root-sum-square, growing with √N.
  Asymmetry is deliberately excluded from RMS — a fixed-sign bias does not
  belong in a root-sum-square of random errors.

This follows the G.8271.1 design approach: split the end-to-end allowance
across the elements that produce error, then sum the allocations.

## Validated

- 5 hops × (50 ns TE + 20 ns asymmetry) → worst case exactly **350 ns**
- RMS of [30, 40, 50] ns → **70.71 ns**
- 350 ns against a 300 ns budget → **FAIL, 50 ns over**
