# Project: First VM — Ubuntu Server on Hyper-V

**Date started:** 2026-08-27
**Status:** Done
**Time spent:** <how long this took you>

## Goal
Set up my Windows 11 Pro PC as a hypervisor using Hyper-V, and build my first
Linux server VM to use as a foundation for future lab projects.

## Environment
- Host: Windows 11 Pro, Hyper-V
- Guest: Ubuntu Server 24.04 LTS (Generation 2 VM)
- Resources: 4 GB RAM (dynamic), 40 GB disk (LVM)
- Networking: Hyper-V External switch bound to Wi-Fi adapter

## Setup
1. Enabled Hyper-V via Windows Features, rebooted.
2. Created an External virtual switch on the Wi-Fi adapter.
3. Created a Gen 2 VM (4 GB RAM, 40 GB disk).
4. Changed Secure Boot template to "Microsoft UEFI Certificate Authority"
   so the Ubuntu bootloader would pass verification.
5. Installed Ubuntu Server with LVM, OpenSSH server enabled.
6. Patched the system: sudo apt update && sudo apt upgrade -y
7. Connected remotely over SSH from PowerShell.

## Result
Working headless Ubuntu server, administered remotely over SSH.
Server IP: 192.168.1.213 (DHCP — may change on reboot; static IP is a
future project).
