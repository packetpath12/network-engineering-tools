# BGP Toolkit

Nine BGP workflows in one page, with live data from the RIPEstat API:

- **Hijack verdict** (default tab) — paste a prefix you own; get a plain-English
  HEALTHY / NEEDS ATTENTION / SUSPICIOUS verdict from origin-ASN count (MOAS),
  more-specifics by others, RPKI validity, IRR/routing consistency, and RIS
  propagation. Handles legitimate MOAS honestly (anycast, multihoming, DDoS
  scrubbing); optional "expected origin ASNs" input. Never claims "hijacked".

- **Prefix lookup** — origin ASNs + holders, announced yes/no, RIR allocation,
  related more/less-specifics.

- **AS lookup** — holder and announced prefixes for any ASN.

- **Looking glass** — per-collector RIS views with sample AS paths.

- **RPKI check** — validate a (prefix, origin ASN) pair against published ROAs.
  Shows the covering ROA(s) and warns when a ROA's maxLength is overly
  permissive — the misconfiguration behind the Aug 2026 RPKI-"valid" hijack
  (a ROA covering a /16 with maxLength /24 authorizes any /24 inside it,
  including an attacker's).

- **Bogon check** — against Team Cymru fullbogons (2026-10-03), baked into the
  page; works offline.

- **Community decoder** — curated, sourced DB (IANA/RFC + NTT, Arelion, Lumen,
  Cogent…); unknown communities are labeled "not in database", never guessed.

- **Propagation tracker** — % of RIS collectors seeing a new announcement.

- **Filter generator** — peer ASN to ready-to-paste IOS-XE + JunOS prefix-lists.

**Live version:**
[allaboutitinfrastructure.com/tools/bgp-toolkit/](https://allaboutitinfrastructure.com/tools/bgp-toolkit/)

**Run it:** open `index.html` in any browser. Single file, no dependencies.
Live lookups call `stat.ripe.net` from your browser (nothing passes through a
server); the bogon check and community decoder work fully offline.

## Honest scope

Verdicts are heuristic — BGP has legitimate reasons for multi-origin
announcements, so results explain rather than alarm. Always correlate with
your own routers before acting. Filter output does not expand IRR as-sets;
expand those with bgpq4/bgpq3 and verify before applying.
