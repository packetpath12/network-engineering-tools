# iPerf3 Command Builder

Generate correct `iperf3` command lines without memorizing flags: pick a role
(client or server), set duration, parallel streams, TCP/UDP, target bandwidth,
window size, DSCP/TOS marking, reverse and bidirectional modes — and get a live
terminal-style preview you can copy. A gotcha linter catches the classic
mistakes (UDP without `-b`, reverse+bidirectional redundancy, windows too small
for high-BDP paths), every emitted flag is explained in plain English, and
presets cover the five jobs people actually run: 1G baselines, UDP loss tests,
10G multi-stream runs, reverse-direction checks, and persistent server daemons.

**Live version:**
[allaboutitinfrastructure.com/tools/iperf3-builder/](https://allaboutitinfrastructure.com/tools/iperf3-builder/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

Stick to real iperf3 3.x flags; `--bidir` and `--cport` need iperf 3.9+.
Windows iperf3 builds lag the Linux releases slightly. The builder generates
commands — it does not run tests or interpret results for you (the
results-interpretation card on the page shows what to look for).
