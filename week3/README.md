# CET1617 Week 3 interactive topic artifacts

Four standalone HTML files, one per session topic. Each is self-contained: stylesheet, GSAP, the
NetLab console (now with IP services), and the topic script are all inlined. No shared assets and
no build step, so any file works on its own from any URL and from local disk.

CBT Technology Institute, Flagler Campus. Prof. Luis De Leon.

| File | Topic | Session |
|---|---|---|
| `w3s1-dhcp-server.html` | 3.1 DHCPv4: the router as the address server | W3S1 |
| `w3s2-dhcp-relay.html` | 3.2 DHCP relay and the router as a DHCP client | W3S2 |
| `w3s3-nat-pat.html` | 3.3 NAT and PAT: private addresses meet the internet | W3S3 |
| `w3s4-hsrp.html` | 3.4 HSRP: a default gateway that survives a router failure | W3S4 |

## What the console now does

The console adds IP services to the routing engine. A router can run a DHCPv4 server
(`ip dhcp excluded-address`, `ip dhcp pool` with `network`, `default-router`, `dns-server`),
checks each address before leasing it and logs conflicts, and picks the pool from the interface or
relay address a request arrived on. `ip helper-address` relays requests across the routed network,
and the server must be able to route its answer back. `ip address dhcp` makes a router a DHCP client
that installs a default route with distance 254. PCs set to DHCP use `ipconfig /renew`,
`/release` and `/all`, and fall back to a 169.254 address when no server answers.

NAT follows IOS: interface roles with `ip nat inside` and `ip nat outside`, standard ACLs to select
traffic, static NAT in both directions, dynamic pools that run out, and PAT with port numbers, with
`show ip nat translations` and `show ip nat statistics`. A reply to an untranslated private address
dies at the provider, as it does on the internet.

HSRP elects an active and a standby router by priority and then address, answers for the virtual
IP only on the active router, fails over when a router is powered off, and preempts only when
`standby N preempt` is set. `show standby brief` and `show standby` report the group, and
`%HSRP-6-STATECHANGE` messages appear as roles change.

- Topic 3.1: Build a DHCP server for two LANs, meet a printer conflict, and a DORA stepper.
- Topic 3.2: Relay two LANs to a central server, bring up the provider link by DHCP, and a lease
  predictor.
- Topic 3.3: Watch a reply die at the ISP, then publish a server, exhaust a pool, and finish with PAT.
  Includes an address-name classifier.
- Topic 3.4: Build an HSRP pair, power off the active router mid-ping, and find the DHCP pool that
  still points at a real router address. Includes an election and failover simulator.

Each file closes with three self-check questions that map to the Week 3 quiz. Demonstration values
use student number 7.
