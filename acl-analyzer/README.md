# Firewall / ACL Rule Analyzer

Paste a Cisco IOS extended ACL or a Juniper firewall filter and this page
reads it the way the firewall does — top-down, first match wins — and flags
the rules that can never fire, the duplicates that add nothing, and the one
line that quietly opens everything.

**Live version:**
[allaboutitinfrastructure.com/tools/acl-analyzer/](https://allaboutitinfrastructure.com/tools/acl-analyzer/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. The analysis runs locally — your ACL never leaves the page.

## How to use

Pick **Cisco IOS** or **Juniper** at the top of the page, then paste:

- Cisco: numbered extended ACL lines
  (`access-list 101 permit tcp any any eq 80`) or bare `permit`/`deny` lines
  from a named ACL.
- Juniper: `set firewall family inet filter ...` lines or a
  `show configuration`-style brace-format firewall filter.

Hit **Analyze**. Findings update live as you type. Each rule gets one verdict:

- **Shadowed** — an earlier rule with the *opposite* action already matches
  every packet this rule could see. The line can never fire; the intent it
  documents is not what the firewall enforces.
- **Redundant** — an earlier rule with the *same* action fully covers it.
  Delete it and the firewall behaves identically.
- **Overly broad** — a `permit ip any any`: every protocol, any source, any
  destination. Anything not explicitly denied above it is open.
- **Clean** — reachable, and doing work no earlier rule already does for it.

## The logic, in brief

Each line is parsed into action, protocol, source range, destination range
(IPv4, wildcard masks applied bit-for-bit per octet, discontiguous masks
included), and port range (`eq`, `range`, `gt`, `lt` modeled; `neq` and unknown
operators treated as the full port range with a note). Rules are evaluated
top-down: a rule is covered by an earlier rule when protocol, both address
ranges, and the port range are all contained. Shadowed rules are excluded as
cover candidates — a dead rule can never match traffic, so it cannot cover
anything. Protocol `ip` correctly covers tcp, udp, and icmp. Only full
containment is reported; partial overlaps are deliberately not flagged.

**Parser scope:** numbered extended IOS ACLs and bare permit/deny lines, IPv4
only; Juniper `family inet` filters (set-format and brace-format). Juniper
terms model source/destination address (CIDR), source/destination port (single,
list, range), protocol, icmp-type, and tcp-established; `then accept` /
`then discard` / `then reject` map to permit/deny, `then next term` is noted
and excluded from verdicts, prefix-lists are noted as not expanded. Not
modeled: object-groups, `time-range` schedules, NAT/route-map interactions,
ASA/FTD syntax, `family inet6`.

## Validated

On the canonical 4-rule test ACL (`permit tcp any host 10.0.0.1 eq 80` /
`deny tcp any host 10.0.0.1 eq 80` / `permit tcp any host 10.0.0.1 eq 80` /
`permit ip any any`): rule 2 → **SHADOWED**, rule 3 → **REDUNDANT**,
rule 4 → **OVERLY BROAD**, rule 1 clean. A clean 3-rule ACL → **zero findings**.
