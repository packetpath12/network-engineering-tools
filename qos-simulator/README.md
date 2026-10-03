# QoS Token-Bucket Policer & Shaper Simulator

Set CIR, Bc, and Be the way you would on a Cisco MQC policy, pick a mode
(single-rate two/three-color or two-rate three-color policer, average/peak
shaper), inject traffic — and watch conform/exceed/violate coloring, shaping
delay, derived Tc, and the exact IOS CLI (`class-map` / `policy-map` /
`police` / `shape` / `service-policy`) with `show policy-map interface`-style
counters.

**Live version:**
[allaboutitinfrastructure.com/tools/qos-simulator/](https://allaboutitinfrastructure.com/tools/qos-simulator/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## Honest scope

Simplified single-flow model: one class, one bucket. Real MQC policies stack
class hierarchies, CBWFQ/LLQ scheduling, and WRED on top of this, and none of
that is modeled here. Token accounting follows Cisco's documented
single-rate/dual-rate behavior.
