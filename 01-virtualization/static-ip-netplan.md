# Project: Static IP via Netplan

**Date:** 2026-08-27
**Status:** Done

## Goal
Give the Ubuntu server a fixed IP so SSH and services don't break when DHCP
reassigns the address.

## Concepts
- Every device needs 4 things: IP, subnet mask, gateway, DNS
- DHCP (automatic, can change) vs static (manual, fixed) — servers use static
- Chose 192.168.1.10: low number, outside the router's DHCP pool, avoids conflicts

## Steps
1. Read current values: ip addr / ip route / resolvectl status
2. Edited /etc/netplan/00-installer-config.yaml (dhcp off, static address,
   route, nameserver), kept the mac match/set-name block
3. Validated with: sudo netplan generate
4. Applied with: sudo netplan apply, reconnected on the new IP

## What broke / what I learned
- YAML indentation errors (missing "- " on the route, misspelled "addresses")
  — netplan generate catches these before they hit the live network
- Mid-edit the VM hit an OOM event and dropped my SSH session; free -h showed
  memory was fine after, so it was a transient Dynamic Memory spike
- netplan try auto-reverts after 120s (safety net) but doesn't help when the
  IP itself changes, since the session drops regardless — used apply + reconnect

## Result
Server reachable at a fixed 192.168.1.10; "dynamic" flag gone from ip addr.