# Data Center Fabric Designer (Clos / Spine-Leaf Generator)

Turn a server count and switch choices into a complete Clos fabric design:
leaf/spine counts and oversubscription, a full per-pair cabling matrix, a BGP
ASN plan, a point-to-point /31 IP addressing plan, an EVPN/VNI overlay plan,
failure analysis (lose a spine / lose a leaf), a 3-stage super-spine
escalation when the fabric outgrows one spine layer, and copy-ready switch
config for Arista EOS, Cisco NX-OS, or SONiC/FRR.

**Live version:**
[allaboutitinfrastructure.com/tools/clos-fabric-designer/](https://allaboutitinfrastructure.com/tools/clos-fabric-designer/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Worked example

Starter AI pod preset: 384 servers, one 100 Gbps NIC each, leaves with 48
downlinks and 8 uplinks at 400 Gbps → 8 leaves, 8 spines, 1.50:1
oversubscription, 64 leaf↔spine cables; losing one spine raises
oversubscription to 1.71:1.

## Honest boundaries

Two-stage designs assume each leaf connects once to every spine. Server
links land on one leaf each (no dual-homing/MLAG modeling). Bisection is a
ceiling estimate, not a traffic promise. Config snippets are generic
BGP/interface/loopback basics to adapt, not a substitute for vendor docs.
