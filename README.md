# CET1617 Week 1 interactive topic artifacts

Four standalone HTML files, one per session topic. Each is completely self-contained: stylesheet,
GSAP, the NetLab routing console, and the topic script are all inlined. No shared assets and no
build step, so any file works on its own from any URL and from local disk.

CBT Technology Institute, Flagler Campus. Prof. Luis De Leon.

| File | Topic | Session |
|---|---|---|
| `w1s1-routing-table.html` | 1.1 How a router decides: reading the routing table | W1S1 |
| `w1s2-static-forms-default.html` | 1.2 Static route forms and the default route | W1S2 |
| `w1s3-floating-static.html` | 1.3 Administrative distance and floating static routes | W1S3 |
| `w1s4-ipv6-static.html` | 1.4 IPv6 static routing | W1S4 |

## What students actually do

Every file contains a practice console that accepts real IOS syntax for the Week 1 routing command
set (interfaces, `ip route` in all three forms with an optional distance, `ipv6 route`,
`ipv6 unicast-routing`, the `show` commands, `ping`, `traceroute`) and rejects everything else the
way a router would, including `%Invalid next hop address (it's this router)`,
`%Inconsistent address and mask`, and `% Interface has to be specified for a link-local nexthop`.
The PCs have their own console with `ipconfig`, `ping` and `tracert`.

Forwarding is simulated hop by hop in both directions. A missing return route fails the ping the
way it does in Packet Tracer (timed out rather than unreachable), traceroute hops without a route
back show as `*`, and every failure prints a `NetLab note` naming the router and the reason.
The topology redraws from live interface state and animates each ping along its real path.

- **1.1** Bring up a link, add a one-way static route, watch the reply die at R2, add the return
  route. A longest-prefix explorer shows which of five overlapping entries wins for six destinations.
- **1.2** Branch, HQ and ISP edge: a default route on the stub, a fully specified route back at HQ,
  a default to the ISP, proven by ping and traceroute. An install predictor covers six commands
  that are installed, accepted but not installed, or rejected.
- **1.3** A triangle with a cable you can cut by clicking it. Build primary and floating routes in
  both directions, cut the cable, ping through the backup, restore it, and trace the path back.
  A distance ranking panel shows which source wins for one prefix.
- **1.4** IPv6 across three routers with hand-set link-local addresses. Hit the link-local error,
  fix it, and find the transit router that is not forwarding. An IPv6 install predictor follows.

Each file closes with three self-check questions that give per-answer feedback and map to the
Week 1 quiz (the answer key lists the mapping). Demonstration values use student number 7.

## Deploying and embedding

1. Push the four files to your repository and enable GitHub Pages.
2. In the Canvas page, click the `</>` icon to open HTML view and paste the snippet from
   `canvas-embed-snippets.html` for that topic, after replacing `USERNAME.github.io/REPO`.

A cross-origin iframe cannot resize itself, so the height is fixed at 2600px, which fits a
desktop browser; the frame scrolls internally below that. Keep the new-tab link underneath: it is
what most students on phones will use. On a phone the topology diagram scrolls sideways inside
its own box, and the page itself never scrolls horizontally.

If your Canvas admin has Content Security Policy enabled under Settings, Security, add
`USERNAME.github.io` to the allowed domains or the frame renders blank. Test one page first.

After updating a file, append a version query to the iframe source, for example `?v=2`, so students
receive the new copy rather than a cached one.

## Accessibility

Console output and status lines are `aria-live` regions, every control is keyboard operable
(including the cuttable cable in 1.3, which also has its own button), and
`prefers-reduced-motion` is honoured: animations resolve instantly and the text still updates.
Nothing is conveyed by motion or colour alone. Every state change is also stated in words.

## Licensing

GSAP 3.15.0 is by GreenSock, bundled under the GSAP standard license rather than pulled from a CDN,
so the pages make no external requests at all.
