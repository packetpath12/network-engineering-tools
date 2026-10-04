# Packet Path — Free Network Engineering Tools

Open-source interactive tools for network engineers, from
[Packet Path](https://allaboutitinfrastructure.com) (free network-engineering
guides and calculators). Each tool is a **single self-contained HTML file** —
no build step, no dependencies, no server. Open it in a browser and it works,
offline included. Everything runs locally; nothing you type ever leaves the page.

## The tools

| Tool | What it does | Live version |
|---|---|---|
| [subnet](subnet/) | **Subnet / CIDR Calculator** — subnet details, binary views, CIDR-to-range tables, same-subnet checks. | [allaboutitinfrastructure.com/tools/subnet/](https://allaboutitinfrastructure.com/tools/subnet/) |
| [bdp](bdp/) | **Bandwidth-Delay Product Calculator** — TCP window sizing, Mathis throughput bounds under loss, packet rates, file-transfer times. | [allaboutitinfrastructure.com/tools/bdp/](https://allaboutitinfrastructure.com/tools/bdp/) |
| [quiz](quiz/) | **Subnet Quiz** — endless CCNA-style practice: network addresses, broadcasts, host counts, VLAN-range questions with explanations. | [allaboutitinfrastructure.com/tools/quiz/](https://allaboutitinfrastructure.com/tools/quiz/) |
| [sla](sla/) | **Availability / SLA Calculator** — what an SLA percentage actually allows in downtime, and what your components add up to. | [allaboutitinfrastructure.com/tools/sla/](https://allaboutitinfrastructure.com/tools/sla/) |
| [dcap](dcap/) | **Data-Center Capacity Planner** — size a spine-leaf fabric: servers per leaf, uplinks, oversubscription, bisection estimates. | [allaboutitinfrastructure.com/tools/dcap/](https://allaboutitinfrastructure.com/tools/dcap/) |
| [ttt](ttt/) | **Tick-to-Trade Latency Calculator** — build the path from market tick to order: propagation, serialization, switch hops, feed handling. | [allaboutitinfrastructure.com/tools/ttt/](https://allaboutitinfrastructure.com/tools/ttt/) |
| [optic](optic/) | **Optical Link Budget Calculator** — power budget, per-element losses, link margin, max reach, with realistic fiber presets. | [allaboutitinfrastructure.com/tools/optic/](https://allaboutitinfrastructure.com/tools/optic/) |
| [ptp-budget](ptp-budget/) | **PTP timing budget calculator** — IEEE 1588 timing-chain budget: worst-case and RMS accumulated time error across N boundary clocks with per-hop asymmetry, checked against 5G fronthaul, MiFID II, and power-utility budgets. | [allaboutitinfrastructure.com/tools/ptp-budget/](https://allaboutitinfrastructure.com/tools/ptp-budget/) |
| [ecmp-hash](ecmp-hash/) | **ECMP hash polarization visualizer** — simulates ECMP hashing across a two-stage Clos fabric; shows how identical hash seeds polarize traffic onto a diagonal of hot paths and how per-switch seed variation restores uniform spreading. | [allaboutitinfrastructure.com/tools/ecmp-hash/](https://allaboutitinfrastructure.com/tools/ecmp-hash/) |
| [acl-analyzer](acl-analyzer/) | **Firewall / ACL rule analyzer** — paste a Cisco IOS extended ACL; detects SHADOWED rules that can never fire, REDUNDANT duplicates, and OVERLY BROAD `permit ip any any` lines. | [allaboutitinfrastructure.com/tools/acl-analyzer/](https://allaboutitinfrastructure.com/tools/acl-analyzer/) |
| [timing-sim](timing-sim/) | **PTP/SyncE network-wide timing simulator** — draw a timing chain (grandmaster, boundary/transparent/slave clocks), then simulate hours of PTP time error: PI servo wander, per-hop asymmetry bias, PDV noise, holdover drift, and ITU-T G.8273.2 Class A–D checks. | [allaboutitinfrastructure.com/tools/timing-sim/](https://allaboutitinfrastructure.com/tools/timing-sim/) |
| [config-verify](config-verify/) | **Network config verifier** — paste Cisco IOS configs; get topology, reachability, and consistency checks: duplicate IPs, OSPF/BGP mismatches, unreachable subnets, and ACL findings. v1: Cisco IOS only, IPv4-only. | [allaboutitinfrastructure.com/tools/config-verify/](https://allaboutitinfrastructure.com/tools/config-verify/) |
| [wireshark-filter-builder](wireshark-filter-builder/) | **Wireshark display filter builder** — build valid display filters without memorizing syntax: 145-field picker, AND/OR/NOT grouping, gotcha linter, plain-English readout, shareable filter links. | [allaboutitinfrastructure.com/tools/wireshark-filter-builder/](https://allaboutitinfrastructure.com/tools/wireshark-filter-builder/) |
| [wifi-planner](wifi-planner/) | **Wi-Fi channel interference planner** — enter audible APs (band, channel, width, RSSI); get spectral overlap graphs, ranked 2.4/5/6 GHz channel recommendations, and a printable multi-AP channel plan. | [allaboutitinfrastructure.com/tools/wifi-planner/](https://allaboutitinfrastructure.com/tools/wifi-planner/) |
| [qos-simulator](qos-simulator/) | **QoS token-bucket policer & shaper simulator** — set CIR/Bc/Be like a Cisco MQC policy, inject traffic, watch conform/exceed/violate coloring and shaping delay, with the exact IOS CLI. | [allaboutitinfrastructure.com/tools/qos-simulator/](https://allaboutitinfrastructure.com/tools/qos-simulator/) |
| [bgp-toolkit](bgp-toolkit/) |
| [iperf3-builder](iperf3-builder/) | **iPerf3 Command Builder** — generate correct iperf3 command lines without memorizing flags: client/server roles, streams, UDP bandwidth, DSCP, reverse/bidir modes, gotcha linter, per-flag explanations, and presets for the jobs people actually run. | [allaboutitinfrastructure.com/tools/iperf3-builder/](https://allaboutitinfrastructure.com/tools/iperf3-builder/) | **BGP Toolkit** — one-click hijack verdict for any prefix (MOAS, more-specifics, RPKI, IRR, propagation), plus prefix/AS lookup, looking glass, RPKI check, bogon check, community decoder, propagation tracker, and IOS-XE/JunOS filter generator — live RIPEstat data. | [allaboutitinfrastructure.com/tools/bgp-toolkit/](https://allaboutitinfrastructure.com/tools/bgp-toolkit/) |

## Use

Open any tool's `index.html` directly in a browser, or serve this repo with any
static file server. Each tool also lives on the Packet Path site (links above),
where it sits alongside the guides that explain the concepts behind it.

## License

MIT License — use these tools, fork them, and embed them wherever they help.
See [LICENSE](LICENSE) for the full text.
