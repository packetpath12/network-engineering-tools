# Packet Path — Free Network Engineering Tools

Open-source interactive tools for network engineers, from
[Packet Path](https://allaboutitinfrastructure.com) (free network-engineering
guides and calculators). Each tool is a **single self-contained HTML file** —
no build step, no dependencies, no server. Open it in a browser and it works,
offline included. Everything runs locally; nothing you type ever leaves the page.

## The tools

| Tool | What it does | Live version |
|---|---|---|
| [ptp-budget](ptp-budget/) | **PTP timing budget calculator** — IEEE 1588 timing-chain budget: worst-case and RMS accumulated time error across N boundary clocks with per-hop asymmetry, checked against 5G fronthaul, MiFID II, and power-utility budgets. | [allaboutitinfrastructure.com/#/tools/ptp-budget](https://allaboutitinfrastructure.com/#/tools/ptp-budget) |
| [ecmp-hash](ecmp-hash/) | **ECMP hash polarization visualizer** — simulates ECMP hashing across a two-stage Clos fabric; shows how identical hash seeds polarize traffic onto a diagonal of hot paths and how per-switch seed variation restores uniform spreading. | [allaboutitinfrastructure.com/#/tools/ecmp-hash](https://allaboutitinfrastructure.com/#/tools/ecmp-hash) |
| [acl-analyzer](acl-analyzer/) | **Firewall / ACL rule analyzer** — paste a Cisco IOS extended ACL; detects SHADOWED rules that can never fire, REDUNDANT duplicates, and OVERLY BROAD `permit ip any any` lines. | [allaboutitinfrastructure.com/#/tools/acl-analyzer](https://allaboutitinfrastructure.com/#/tools/acl-analyzer) |

## Use

Open any tool's `index.html` directly in a browser, or serve this repo with any
static file server. Each tool also lives on the Packet Path site (links above),
where it sits alongside the guides that explain the concepts behind it.

## License

MIT License — use these tools, fork them, and embed them wherever they help.
See [LICENSE](LICENSE) for the full text.
