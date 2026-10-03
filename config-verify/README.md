# Network Config Verifier

Paste Cisco IOS device configs and get topology, reachability, and
consistency verification — the "digital-twin scoped" v1: a browser tool that
checks what your configs *actually* say before you push them.

**Live version:**
[allaboutitinfrastructure.com/tools/config-verify/](https://allaboutitinfrastructure.com/tools/config-verify/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

> **v1 scope, stated honestly:** Cisco IOS only, IPv4 only, simplified RIB
> derivation (connected + static + OSPF/BGP-advertised prefixes). It verifies
> the configs you paste — it does not emulate device forwarding behavior.

## How to use

1. **Paste configs** — one pane per device; add or remove panes as needed.
   Or hit **Load sample lab** for a clean 3-router example.
2. **Run verification** — analysis runs as you type. Each pane header shows
   the parsed device name and a summary.
3. **Read the findings** — every finding names the devices, interfaces, and
   addresses involved and explains *why* it matters in plain English. You
   also get a topology view derived from shared subnets and per-device
   parsed summaries.

## The five checks

1. **Duplicate IP addresses** — the same address configured on two devices.
   Whichever ARP entry wins decides where traffic goes: flapping or
   blackholing.
2. **OSPF area / hello / dead-timer mismatch** — on a shared link, neighbors
   must agree on area and timers or the adjacency never forms.
3. **BGP remote-AS mismatch** — each side's `remote-as` must match the
   neighbor's actual ASN, or the session stays idle.
4. **Unreachable subnets** — a subnet with no route via connected, static,
   or advertised prefixes from a given device.
5. **ACL findings** — extended ACLs are run through the same analyzer as the
   [ACL rule analyzer](../acl-analyzer/): shadowed rules that can never fire,
   redundant duplicates, and overly broad `permit ip any any` lines.

## Validated

Against the shipped parser + checker, on hand-built 3-router config sets:

- Dirty set (1 duplicate IP + 1 OSPF area mismatch + 1 BGP remote-AS
  mismatch planted) → exactly **1 dup-ip + 1 ospf-area + 1 bgp-asn**
  finding, zero others
- Clean 3-router set → **zero findings** across all checks
