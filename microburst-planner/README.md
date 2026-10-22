# Microburst Buffer Planner

Will this switch drop that burst? Enter a synchronised microburst — senders,
burst size, sender and egress rates — and get the peak queue and how long the
last byte waits. Then size the shared buffer pool across ports: static
fits/drops verdicts with pool-fill time and dropped bytes, or dynamic
thresholds (alpha) with the closed-form equilibrium
q = alpha*P / (1 + alpha*K). Pool presets include a generic 16 MiB default and
datasheet classes (Arista 7050SX 12 MB, 7050X3 32 MB, 7050X4 up to 132 MB,
Cisco Nexus 9300-EX/FX 40 MB — vendor MB figures are kept in MB, never
relabelled as MiB). Fluid model, synchronised worst case; planning estimates,
not lab measurements. No ECN/PFC (see the RoCEv2 planner) and no token
buckets (see the QoS simulator).

**Live version:**
[allaboutitinfrastructure.com/tools/microburst-planner/](https://allaboutitinfrastructure.com/tools/microburst-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Start with the default: 32 senders x 64 KiB at 100 Gb/s into a 100 Gb/s
   egress — peak queue 2,031,616 bytes, last byte waits about 162.5 us.
2. Add a static queue cap to see when it fills (t_fill) and how many bytes drop.
3. Switch to the shared-pool section when several ports burst at once, and try
   alpha mode to see how much of the pool one queue may hold.
