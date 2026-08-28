# Project: SSH Key-Based Authentication

**Date:** 2026-08-28
**Status:** Done (password auth still enabled — disabling it is the next step)
**Time spent:** <fill in>

## Goal
Replace password login to the Ubuntu server with SSH key-based authentication —
more secure, and the standard way servers are accessed.

## Concepts
- Key pair = private key (stays on my PC, never sent anywhere) + public key
  (copied to the server, safe to share).
- The private key never crosses the network. The server issues a challenge only
  the matching private key can answer; my PC sends back proof, not the key itself.
- More secure than a password because the secret never travels, and the keys are
  too large to brute-force.
- Used ed25519 (modern, fast, secure) rather than older RSA.
- SSH finds the key automatically because it was saved with the default name
  (id_ed25519) in the default folder (~/.ssh) — convention on both ends.

## Steps
1. Generated a key pair on the Windows PC:
   ssh-keygen -t ed25519 -C "homelab-key"
   (accepted default filename/location; no passphrase)
2. Copied the public key to the server's ~/.ssh/authorized_keys via a piped
   one-liner, which also set the strict permissions SSH requires
   (700 on ~/.ssh, 600 on authorized_keys).
3. Tested: ssh jon@192.168.1.10 — logged in with no password prompt.

## What broke / what I learned
- Hit a connection issue when first testing key login: typo within the Ip address, but fixed after a second glance.
- Learned SSH refuses to use keys if the .ssh folder/authorized_keys permissions
  are too open — the chmod 700/600 steps aren't optional, they're a security check.
- Learned the difference between a key passphrase (unlocks the private key locally)
  and a server password (sent over the network) — different things.

## Result
Key-based login works to 192.168.1.10 with no password prompt. Public key is on
the server's allow-list; private key stays on the PC.
