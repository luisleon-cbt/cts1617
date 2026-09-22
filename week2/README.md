# CET1617 Week 2 interactive topic artifacts

Four standalone HTML files, one per session topic. Each is self-contained: stylesheet, GSAP, the
NetLab console (now with OSPF), and the topic script are all inlined. No shared assets and no
build step, so any file works on its own from any URL and from local disk.

CBT Technology Institute, Flagler Campus. Prof. Luis De Leon.

| File | Topic | Session |
|---|---|---|
| `w2s1-ospf-neighbors.html` | 2.1 How OSPF works: neighbors, router IDs, and the link-state database | W2S1 |
| `w2s2-ospf-configuration.html` | 2.2 Configuring single-area OSPFv2 and reading OSPF routes | W2S2 |
| `w2s3-dr-bdr-cost.html` | 2.3 DR and BDR election, network types, and cost | W2S3 |
| `w2s4-ospf-default-troubleshooting.html` | 2.4 Default routes in OSPF and troubleshooting adjacencies | W2S4 |

## What the console now does

The console runs single-area OSPFv2: `router ospf`, `router-id`, `network` with wildcards,
`ip ospf N area 0` in interface mode, `passive-interface` (and `default`),
`default-information originate`, `auto-cost reference-bandwidth`, and the interface commands
`ip ospf cost`, `priority`, `hello-interval`, `dead-interval` and `network point-to-point`.
Neighbors form only when area, subnet and mask, timers and router IDs agree and neither side is
passive, and `show ip ospf neighbor` adds a NetLab note naming any mismatch it finds. DR and BDR
elections on shared segments are non-preemptive, as in IOS, until `clear ip ospf process`.
SPF uses real interface costs with equal-cost multipath, and `%OSPF-5-ADJCHG` messages appear
as adjacencies come and go. Switches create shared segments, and a cable cut beyond a switch
leaves the router's own interface up, which is how Topic 2.4 shows a static route blackholing
where OSPF reroutes.

- **2.1** Bring up OSPF on the Week 1 triangle with no static routes, plus a neighbor-state
  stepper from Down to Full.
- **2.2** Add a router with interface-mode OSPF, make LANs passive, advertise a loopback, and use a
  wildcard matcher on R1's interfaces.
- **2.3** Four routers on one switch elected the "wrong" DR. Fix it with priority and clears,
  then steer traffic with cost. Includes an election simulator and a cost calculator.
- **2.4** Originate a default route, fix a timer mismatch, then cut a cable beyond a switch and
  compare OSPF with a leftover static route. Includes an adjacency doctor.

Each file closes with three self-check questions that map to the Week 2 quiz. Demonstration values
use student number 7.

## Deploying and embedding

Same as Week 1: push the files to GitHub Pages and paste the snippets from
`canvas-embed-snippets.html` after replacing `USERNAME.github.io/REPO`. Heights are fixed at
2800px because these pages are longer. Keep the new-tab link underneath for phones. If your
Canvas admin has Content Security Policy enabled, `USERNAME.github.io` must be on the allowed list.
After updating a file, append `?v=2` to the iframe source to defeat caching.

## Accessibility

Console output and status lines are `aria-live` regions, every control is keyboard operable
(including the cuttable cable in 2.4, which also has its own button), `prefers-reduced-motion`
is honoured, and every state change is stated in words, including the current DR and BDR in 2.3.

## Licensing

GSAP 3.15.0 is by GreenSock, bundled under the GSAP standard license.
