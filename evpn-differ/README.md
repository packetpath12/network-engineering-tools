# EVPN Two-VTEP Route Differ

Paste `show bgp l2vpn evpn` output from two VTEPs and get one plain-English verdict on whether the two ends agree — per VNI, per route type — with the route lines from both ends shown as evidence for every finding. EVPN's classic failure mode is "works one way"; a single-device decoder cannot see it.

It parses NX-OS and EOS bracket-NLRI output, decodes route types 1–5, and classifies disagreements: Type-3 IMET missing one way, Type-2 hosts visible one way only, Route Target mismatches (import is driven by RT, so a mismatch silently installs nothing), VNI/label mismatches, one-way Type-5 prefixes, duplicate RDs, ESI/DF inconsistencies and MAC-mobility conflicts. Different Route Distinguishers on the two ends are normal and are never flagged — the only RD fault is the same RD on both VTEPs for the same EVI. JunOS/FRR output shapes are detected and honestly reported as not yet supported.

**Live version:**
[allaboutitinfrastructure.com/tools/evpn-differ/](https://allaboutitinfrastructure.com/tools/evpn-differ/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. 100% client-side — pasted output never leaves your browser. It does not connect to any device or monitor a fabric.

## How to use

1. On each VTEP, run `show bgp l2vpn evpn` and paste the output into its box.
2. Or click a demo preset: Symmetric pair (the two ends agree) or Broken pair (exactly 3 planted faults).
3. Read the headline verdict first, then each classified disagreement with the evidence lines from both ends.
