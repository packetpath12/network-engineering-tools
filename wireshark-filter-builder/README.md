# Wireshark Display Filter Builder

Build valid Wireshark display filters without memorizing syntax. Pick from
145 curated fields with plain-English descriptions, add conditions, combine
with AND/OR/NOT — get a valid filter string, a plain-English readout of what
it matches, a gotcha linter (`!=` multi-value trap, `contains` vs `matches`,
`==` vs `===`), and a shareable link. Includes one-click recipes and a
paste-in expression sanity checker.

**Live version:**
[allaboutitinfrastructure.com/tools/wireshark-filter-builder/](https://allaboutitinfrastructure.com/tools/wireshark-filter-builder/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

This builder covers 145 of the most-used display-filter fields — Wireshark's
full dictionary has over 100,000 — plus the core operators. It is a composer,
not a compiler: always sanity-check the generated filter in Wireshark before
trusting it on a real capture.
