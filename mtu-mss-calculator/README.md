# MTU/MSS Tunnel Overhead Calculator

Stack up GRE, IPsec, VXLAN, GENEVE, MPLS, PPPoE, L2TPv3 or WireGuard headers and
see exactly what they cost: per-layer byte overhead with a running total, the
effective inner MTU, the TCP MSS to configure (with a paste-ready
`ip tcp adjust-mss` command), and a plain-English fragmentation verdict for
your test packet size — including the fragment sizes when it will fragment.
One-click presets cover the jobs people actually run: IPsec site-to-site,
VXLAN overlays, PPPoE DSL + IPsec, MPLS L3VPN (2 labels), and WireGuard
tunnels. IPsec ESP padding is recomputed live per packet size, because unlike
every other header here it isn't fixed.

**Live version:**
[allaboutitinfrastructure.com/tools/mtu-mss-calculator/](https://allaboutitinfrastructure.com/tools/mtu-mss-calculator/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

Every overhead figure is documented in the page and defensible: Ethernet II
14 (+4 802.1Q), IPv4 20, IPv6 40, UDP 8, GRE 4 (+4 key, +4 seq per RFC
2784/2890), IPsec ESP per RFC 4303 (8 header + IV 16 AES / 8 3DES + computed
padding + 2 trailer + ICV 12 SHA-1 / 16 SHA-256; tunnel mode adds a new 20-byte
outer IPv4 header), VXLAN 50 (RFC 7348), GENEVE 50 + your option bytes
(RFC 8926), MPLS 4 per label (RFC 3032), PPPoE 8 (RFC 2516), L2TPv3-over-IP
4-byte session ID + optional cookie (RFC 3931 — UDP-based deployments are
explicitly not counted), WireGuard 32-byte data message (excludes outer
IP/UDP, added as separate layers). MSS assumes IPv4/TCP inside (minus 40);
IPv6 inside needs minus 60, which the page states. Fragment sizes assume
standard 8-byte-aligned IPv4 fragmentation.
