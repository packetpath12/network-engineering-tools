# BGP Route Reflector Design Planner

Plan an iBGP route-reflector design in one flow: full-mesh vs reflected session math for any cluster layout — flat or two-tier hierarchical — per-router peer lists, cluster-ID validation, blast-radius analysis when reflectors fail, an RFC 4456 reflection walk-through with the loop-prevention discards, and a starter Cisco config.

**Live version:**
[allaboutitinfrastructure.com/tools/bgp-rr-planner/](https://allaboutitinfrastructure.com/tools/bgp-rr-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Start from the four-site campus preset: 4 clusters, each with 2 reflectors + 8 clients (40 routers). A full mesh would need 780 iBGP sessions; the reflected design needs 92.
2. Change the cluster count, reflectors per cluster, and clients per cluster — or enter a total router count and let the tool distribute clients — and watch the session math, peer lists, and verdict update.
3. Use the failure test to fail one reflector, or every reflector in a cluster, and read the blast radius: sessions lost, clients orphaned, clients merely degraded.
4. Edit a cluster-ID to see the validation catch the two classic mistakes: paired reflectors disagreeing on their cluster-ID, and two clusters reusing one ID.
5. Step through the reflection simulation to see ORIGINATOR_ID and CLUSTER_LIST (RFC 4456) being set, checked, and causing discards.
6. Turn on the hierarchy toggle to add a second tier: 2 dedicated top-level reflectors above the clusters. The preset grows from 40 to 42 routers while sessions drop from 92 to 81 (a full mesh of 42 would need 861). Cluster reflectors peer only upward, the top pair peers with each other, and failing both top reflectors isolates the clusters from each other without orphaning any client.

Honest note: this is not the only route-reflector calculator in existence — an installable EVPN-fabric CLI (evpn-ninja) has a basic session calculator. This one is a free web tool with the integrated design package: session math, peer lists, validation, blast radius, and the loop-prevention simulation in one place. The starter config is a starting point, not a validated production config.
