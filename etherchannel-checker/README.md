# EtherChannel / LACP Two-End Bundle Checker

Paste the EtherChannel output from BOTH ends of a bundle — `show etherchannel summary` (IOS/IOS XE), `show port-channel summary` (NX-OS / Arista EOS), neighbor output, interface status, and config snippets — and get a verdict: the exact mismatches that stop a port-channel forming, every member flag decoded in your own output, and copy-ready fix commands for your exact ports.

Checks include protocol mismatch (LACP vs PAgP), passive/passive and auto/auto pairs, static `on` vs negotiating ends (the one-side-bundled blackhole), speed/duplex mismatches, trunk/access mixing, native and allowed VLAN mismatches, suspended/stand-alone member decoding, member-count and split-group pairing breaks, miscabling to two different far-end devices, and Layer 2 vs Layer 3 channel ends.

**Live version:**
[allaboutitinfrastructure.com/tools/etherchannel-checker/](https://allaboutitinfrastructure.com/tools/etherchannel-checker/)

**Run it:** open `index.html` in any browser. Single file, no dependencies, works offline. 100% client-side — pasted output never leaves your browser; the page makes no network calls.

## How to use

1. On Switch A, run `show etherchannel summary` (or `show port-channel summary` on Nexus/Arista) and paste the output into the Switch A box. Add neighbor, interface-status, or config output if you have it.
2. Do the same for Switch B.
3. Read the verdict banner first, then the problem cards — each names the root cause, shows your own evidence lines from both ends, and prints the fix commands.
