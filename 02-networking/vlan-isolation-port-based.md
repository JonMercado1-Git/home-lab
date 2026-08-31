# Project: VLAN Isolation (Port-Based) — NETGEAR GS308Ev4

**Date:** 2026-08-31
**Status:** Done
**Time spent:** <30 mins>

## Goal
Segment a single physical switch into two isolated networks using port-based
VLANs, and prove that devices on different VLANs cannot communicate.

## Concepts
- A VLAN splits one physical switch into multiple separate networks. Ports in
  different VLANs cannot exchange traffic, even on the same hardware.
- This is segmentation — the foundation of network security 
- Started with port-based VLANs (assign ports to groups by number) as the most
  intuitive form before moving to the 802.1Q industry standard.

## Setup
- Switch: NETGEAR GS308Ev4, Basic Port-Based VLAN mode
- Port 1: router (VLAN 1)
- Port 2: management PC (VLAN 1) — kept with router so I wouldn't lock myself out
- Port 3: test laptop (moved between VLAN 1 and VLAN 2)

## Method (baseline -> change -> test -> reverse)
1. Baseline: all ports flat, pinged laptop from PC -> replies (can communicate).
2. Moved laptop to VLAN 2, PC stayed in VLAN 1.
3. Pinged again -> request timed out (isolated). Confirmed both directions.
4. Moved laptop back to VLAN 1.
5. Pinged again -> replies returned (communication restored).

## What I learned
- Same VLAN = devices communicate; different VLAN = blocked, with no other
  change. The VLAN assignment alone controls reachability.
- Kept the management port in the same VLAN as the router to avoid cutting off
  my own access mid-config (same "don't saw off your branch" principle as
  remote SSH changes).
- Establishing a baseline before the change is what proves cause and effect.

## Result
Verified working Layer 2 isolation between two VLANs on one physical switch,
demonstrated bidirectionally and shown to be reversible.

## Next steps
- Reconfigure using 802.1Q VLANs (access/trunk ports, tagging) — the
  professional standard.
- Explore inter-VLAN routing (controlled communication between VLANs via a
  router/firewall).