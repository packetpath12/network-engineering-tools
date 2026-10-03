# Wi-Fi Channel Interference Planner

Enter the access points you can hear — band (2.4/5/6 GHz), channel, width,
RSSI — and get a per-band spectral overlap graph, ranked channel
recommendations with interference scores and reasoning, a greedy multi-AP
channel assignment, and a printable channel plan. Includes DFS warnings and
6 GHz PSC notes, plus US/ETSI/JP regulatory domain selection.

**Live version:**
[allaboutitinfrastructure.com/tools/wifi-planner/](https://allaboutitinfrastructure.com/tools/wifi-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

This planner uses a simplified rectangular-spectrum model: each AP is a flat
block of spectrum, so adjacent-channel leakage is approximate — real 802.11
spectral masks roll off instead of cutting off. It is a planning aid, not an
Ekahau replacement.
