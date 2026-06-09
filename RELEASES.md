# Burrow 0.6.5

A reliability release. The Installers and Purge selection flows no longer hang,
and the code that drives the Mole CLI is now extensively tested.

## Fixes
- **No more "Scanning…" hang.** Two cases that could freeze the Installers/Purge
  tools are fixed: when Mole finds nothing and exits before showing a list, and
  when you scan a second time. Both now resolve cleanly.

## Under the hood
- The interactive selection flow (installer/purge) is now a small, pure state
  machine driven entirely by tests, so the safety-critical "remove exactly what
  you picked — or nothing" logic is verified in CI rather than by hand.
- Reading and parsing Mole's output is consolidated into a few tested modules
  (one ANSI cleaner, one typed client, one snapshot store). No behavior change —
  the app looks and works the same; it's just far harder to regress.
- Test suite grew from 90 to 124.

## Install
```
brew install --cask caezium/tap/burrow
```
Pulls in the `mole` engine and clears the Gatekeeper quarantine for you.
Ad-hoc signed (so Full Disk Access grants stick); not yet notarized.

---
Older releases: see the
[Releases page](https://github.com/caezium/Burrow/releases).
