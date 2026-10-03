# Subnet / CIDR Calculator

Enter an IP and prefix length — get the network address, broadcast,
usable host range, host count, wildcard mask, and a binary breakdown, plus
CIDR-to-range tables and a same-subnet checker for two addresses.

**Live version:**
[allaboutitinfrastructure.com/tools/subnet/](https://allaboutitinfrastructure.com/tools/subnet/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Type an address like `10.20.30.40/22` (CIDR or dotted-mask notation both work).
2. Read the network/broadcast, first/last usable host, total and usable host counts.
3. Flip to the binary view to see exactly which bits are network vs host.
4. Use the same-subnet checker to test whether two addresses share a subnet.
