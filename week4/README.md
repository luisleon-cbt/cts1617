# CET1617 Week 4 interactive topic artifacts

Four standalone HTML files, one per session topic. Each is self-contained: stylesheet, GSAP, the
NetLab console (now with management services), and the topic script are all inlined. No shared
assets and no build step, so any file works on its own from any URL and from local disk.

CBT Technology Institute, Flagler Campus. Prof. Luis De Leon.

| File | Topic | Session |
|---|---|---|
| `w4s1-ssh-access.html` | 4.1 SSH and secure device access | W4S1 |
| `w4s2-ntp-dns.html` | 4.2 NTP and DNS: the right time and the right name | W4S2 |
| `w4s3-syslog-snmp.html` | 4.3 Syslog and SNMP: hearing from your routers | W4S3 |
| `w4s4-qos-managed-edge.html` | 4.4 QoS concepts and the managed edge | W4S4 |

## What the console now does

Device access follows IOS: `enable secret` (hashed in the running configuration),
`service password-encryption`, console and vty lines with `password`, `login`, `login local`,
`transport input` and `exec-timeout`, local usernames, a message of the day banner, and SSH that
needs a hostname, `ip domain-name` and an RSA key (version 2 needs at least 768 bits). From a PC or
a router, `ssh -l USER ADDRESS` and `telnet ADDRESS` open a real session: the console moves onto the
target router, passwords are prompted and not echoed, and `exit` closes the session.

Routers keep a clock that starts in 1993 with the asterisk until NTP synchronizes it. `ntp server`
builds a stratum hierarchy, and `show clock`, `show ntp status` and `show ntp associations` report
it. `ip name-server`, `ip host` and `no ip domain-lookup` behave as in IOS, including the pause on a
mistyped command, and PCs resolve names with `nslookup` and `ping NAME`.

Log messages carry their IOS severity. `logging host`, `logging trap` and
`service timestamps log datetime msec` decide what reaches the syslog server and how it is dated,
and Topic 4.3 shows the server's received messages live. `snmp-server community` answers
`snmp get` requests from the NMS (a stand-in for Packet Tracer's MIB Browser), and a wrong community
gets no answer at all.

- Topic 4.1: Lock down a router after an audit, prove SSH works and telnet is refused, with a
  capture viewer comparing the two protocols.
- Topic 4.2: Synchronize two routers into an NTP hierarchy and make names work, with a log
  correlation exercise showing why NTP matters.
- Topic 4.3: Send logs to a syslog server, filter them by severity, fix a router's dates, and read
  a router over SNMP, with a severity filter explorer.
- Topic 4.4: Bring two routers under management as Skills Check practice, with a QoS congestion
  simulator comparing FIFO, marking, LLQ, policing and shaping.

Each file closes with three self-check questions that map to the Week 4 quiz. Demonstration values
use student number 7.
