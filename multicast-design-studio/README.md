# Multicast Design Studio

Design a PIM multicast network in one flow: shared (RPT) and source (SPT)
trees drawn on a live topology with per-receiver stretch, RP placement
scored for every candidate, the exact RFC 7761 BSR hash computed with
BigInt, an ASM-vs-SSM decision helper, anycast-RP failover, and a starter
Cisco IOS-style config.

**Live version:**
[allaboutitinfrastructure.com/tools/multicast-design-studio/](https://allaboutitinfrastructure.com/tools/multicast-design-studio/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Start with the preset "exchange feed" topology: a 4 Gb/s source at R1 for
   group 239.1.1.1, receivers at R3, R5 and R6.
2. Compare the shared tree and the source tree per receiver (latency and
   stretch), then read the RP placement scoreboard — on the preset, R2 wins
   with 19 ms total shared-tree latency.
3. Run the BSR hash lab to see which candidate RP actually wins a group
   (for 239.1.1.1 with hash-mask length 30, the winner is 10.0.0.3).
4. Use the ASM-vs-SSM helper before designing: a group inside
   232.0.0.0/8 is SSM-only, so RP design is disabled for it.
5. Toggle an anycast-RP failure to see receivers re-join the survivor.

Honest scope: built first for HFT market-data feeds (SSM), with enterprise
media/IPTV as the second audience. The starter config is a starting point,
not a validated production config.
