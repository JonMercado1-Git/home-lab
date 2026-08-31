# Project: Switch Firmware Update — NETGEAR GS308Ev4

**Date:** 2026-08-31
**Status:** Done

## Goal
Update the managed switch's firmware before building on it, to apply security
fixes and start from a current, supported baseline.

## Steps
1. Found current version (V1.0.1.9) on the switch's System/Information page.
2. Identified exact model as GS308Ev4 (firmware numbering differs from base
   GS308E — important, since flashing the wrong model's file can brick it).
3. Confirmed latest version was V1.0.1.13 (security fixes) on NETGEAR's site.
4. Downloaded and unzipped the model-specific firmware.
5. Flashed via System > Maintenance > Firmware Update; switch rebooted itself.
6. Verified it came back up on V1.0.1.13.

## What I learned
- A firmware flash must not be interrupted (power/connection) or the device
  can brick — treated it as a careful, no-touch operation.
- Outdated network-device firmware is a security gap; keeping it current is
  basic hygiene.

## Result
Switch running current firmware V1.0.1.13, ready for VLAN configuration.