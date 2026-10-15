# RoCEv2 Lossless Ethernet Planner (PFC / ECN / DCQCN Tuning Lab)

Tune a lossless RoCEv2 fabric in one flow: validate the ECN threshold ladder
(Kmin / Kmax / Pmax) against your real per-port buffer, compute PFC XOFF
headroom from link speed, cable length and pause-processing time, simulate
incast queue build-up (queue over time, where ECN marks, where PFC fires,
drain time), and catch deadlock / pause-storm risk flags tied to your own
inputs — ECN thresholds set above the physical buffer ("ECN can never fire
before PFC"), XON equal to XOFF, headroom smaller than one max-size frame,
PFC enabled on the CNP priority, and multi-hop cyclic-pause risk. Includes a
copy-ready NVIDIA Spectrum / Cumulus-style config snippet computed from your
numbers.

**Live version:**
[allaboutitinfrastructure.com/tools/rocev2-planner/](https://allaboutitinfrastructure.com/tools/rocev2-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Worked example

100 Gbps link, 100 m cable, 9,000-byte MTU, 2 µs pause processing: round-trip
propagation is 1.0 µs, so the reaction window is 3 µs → 12,500 B/µs × 3 µs =
37.5 KB, plus one jumbo frame in flight → ≈46.5 KB minimum PFC headroom.
Incast check: 32 senders × 256 KiB each → ≈7.75 MiB peak queue, ≈0.65 ms to
drain at line rate.

## Honest boundaries

Planning math, not a lab measurement: thresholds follow the DCQCN model
(Zhu et al., SIGCOMM 2015) and vendor RoCE deployment guidance. The incast
simulation assumes all senders start together with no congestion control
acting yet. Buffer occupancy is dynamic and shared on real silicon — verify
against your switch vendor's current RoCE guide before deploying.
