# L2 Instability Log Analyzer

Paste `show logging` output from one or more switches and get one plain-English verdict on the instability pattern — probable Layer-2 loop, probable bundle mismatch, a gateway fight (FHRP / virtual-MAC movement), a single roaming or duplicated client, or a physically flapping link — with the evidence ranked and the next checks in senior order.

It parses IOS/IOS XE MACFLAP_NOTIF lines, Catalyst 9000 MAC_MOVE lines, Catalyst 4500 HOSTFLAPPING lines, NX-OS L2FM MAC-move and ETHPORT lines, and LINK/LINEPROTO up-down lines. Spanning-tree topology-change lines are shown as context only — per Cisco's TAC loop methodology they mostly identify victims, not the source. Classification classes follow Cisco docs 221140, 221722 and 221191. When a bundle mismatch is the verdict, the tool hands off to the EtherChannel / LACP Two-End Bundle Checker.

**Live version:**
[allaboutitinfrastructure.com/tools/l2-instability-analyzer/](https://allaboutitinfrastructure.com/tools/l2-instability-analyzer/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. 100% client-side — pasted logs never leave your browser; the page makes no network calls. It does not monitor anything or connect to any device.

## How to use

1. On each switch, run `show logging` and paste the output into a box (add more boxes for more switches, up to 6).
2. Or click a demo preset: Clean, Loop, or Gateway fight.
3. Read the headline verdict first, then the ranked evidence groups — each shows the MAC, VLAN, port pair, event count and rate — and follow the fix card's checks in order.
