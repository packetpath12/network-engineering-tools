# Segment Routing Policy Lab

Draw a topology (or load the SP backbone / multi-PoP enterprise presets), edit
IGP/TE metrics, delay, bandwidth, affinity colors and SRLG groups per link,
then define Segment Routing policies and watch the lab work: dynamic candidate
paths computed with CSPF under bandwidth, delay, affinity and hop constraints,
explicit SID lists you type yourself, and an honest winner selection that
shows, per candidate, exactly why it won or which constraint it failed. The
winning SID list is shown as labeled chips, compressed where possible, and
checked against the head-end's Maximum SID Depth (MSD). A TI-LFA tab computes
P-space / Q-space repair paths for a protected link and animates the backup on
the topology; a Flex-Algo tab compares Algo 0 routing against a Flex-Algo
(128–255) with its own metric and affinity exclusions, destination by
destination.

**Live version:**
[allaboutitinfrastructure.com/tools/sr-te-path-lab/](https://allaboutitinfrastructure.com/tools/sr-te-path-lab/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

The computation engine is validated by an automated test suite (45/45 vectors:
CSPF pruning, explicit-path tracing, preference selection, SID compression,
TI-LFA P/Q-space, Flex-Algo). Addressing follows Cisco IOS XR defaults:
node-SIDs from the default SRGB (16000–23999), adjacency SIDs from the SRLB
(15000–15999), MSD default 10. The preference rule follows the IOS XR SR-TE
docs — the candidate path with the **highest** preference wins; equal-preference
tie-breaks (lower computed cost, then dynamic-first) are this lab's stated
rules for repeatable results, not IOS XR behavior. Boundaries, stated on the
page itself: SR-MPLS only (no SRv6), single IGP area/level, one shortest path
per computation (no ECMP per-segment multi-path), TI-LFA is a simplified
P/Q-space model of RFC 7490 (no node/SRLG protection or multiple failures),
delay and bandwidth are static link attributes you set, and Flex-Algo models
metric + affinity-exclude only.
