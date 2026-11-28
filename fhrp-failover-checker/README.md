# FHRP Pair Failover Simulator & Checker

Paste BOTH gateways' HSRP, VRRP or GLBP config or `show` output and get one plain-English verdict — will this pair actually fail over? — with the silent faults named: a track decrement too small to cross, preempt missing on the takeover side, a tie that goes to the wrong box, authentication/version/group mismatches, plus a step-by-step playback of the failure with the priority arithmetic shown.

It parses Cisco IOS/IOS XE interface config (both track syntaxes), `show standby` / `show vrrp` / `show glbp` brief and detail output, `show track`, and NX-OS per-group submode config. Nineteen checks (C1-C19) in a fixed order; only root causes count as problems — observed states attach to the check that explains them, and correct-by-design behaviour (a VRRP address owner at priority 255, a GLBP load-balancing difference, a deliberate preempt delay) is reported as information, never as a fault.

**Live version:**
[allaboutitinfrastructure.com/tools/fhrp-failover-checker/](https://allaboutitinfrastructure.com/tools/fhrp-failover-checker/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. 100% client-side — pasted config never leaves your browser. It does not connect to any device.

## How to use

1. Paste Gateway A's config or show output in the left box, Gateway B's in the right box.
2. Or click a demo preset: Working pair (clean, 0 problems) or Broken pair (exactly 3 planted faults).
3. Read the verdict banner first, then each problem card with evidence lines from both ends and a copy-ready fix, then play the failure in the simulation.
