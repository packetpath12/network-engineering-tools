# CGNAT Port-Block Planner

How many subscribers actually fit behind your public IPs? Enter your public-IP pool, usable port range and port-block size and get the sizing table (blocks per IP, total blocks, stranded ports), guaranteed vs statistical subscriber capacity, per-subscriber waste and utilisation, a logging-volume estimate, and a deterministic reverse lookup that maps a public IP and port back to its subscriber block.

**Live version:**
[allaboutitinfrastructure.com/tools/cgnat-planner/](https://allaboutitinfrastructure.com/tools/cgnat-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Start with the defaults: 16 public IPs, ports 1024–65535, 512-port blocks, 300 peak ports per subscriber. That gives 2,016 blocks and 2,016 guaranteed subscribers (126 per public IP), with 212 ports wasted per subscriber (58.6% utilisation).
2. Change the block size and watch the stranded ports: a block must be contiguous ports on one public IP, so 2,048-port blocks strand 1,024 ports on every IP. The tool shows the stranded remainder instead of hiding it.
3. Compare the guaranteed figure with the statistical one (average blocks actually held) — and read the oversubscription warning beside it. Statistical is only bigger when the average held is below the blocks-per-subscriber figure.
4. Use the reverse lookup when a complaint or lawful request lands: give it the public IP and port and it returns the block range, the global block and the subscriber slot (0-based, labelled). A port in the stranded tail honestly returns UNALLOCATED.

## The model

usable ports = port_end − port_start + 1. Blocks per IP = FLOOR(usable / block size) — per IP, never pooled across IPs, because a block cannot span two addresses. Guaranteed capacity = FLOOR(total blocks / CEIL(peak ports / block size)). Logging volume = subscribers × events per day × record bytes, in decimal GB/TB; deterministic NAT computes the assignment from IP+port, so it needs no per-session allocation logs. The default first IP (203.0.113.0) is an RFC 5737 documentation address, used as an example only.

Honest note: vendor documentation publishes these formulas with static worked examples, but no free web tool was found (October 2026 market check) that runs your own pool, block and logging numbers.
