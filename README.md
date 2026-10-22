# chassis releases

Prebuilt macOS installer releases for [chassis](https://chassis.engineering) —
a small P2P document-and-payments sidecar that powers the
chassis.engineering/nobody.news network. Source lives in a private repo;
this repo holds only built, downloadable release artifacts.

## Install

**Option 1: double-click installer** - download
[chassis-installer.pkg](https://github.com/brianebert/chassis-releases/releases/latest/download/chassis-installer.pkg),
open it, click through. Installs for your user only (no admin password).
Since it's unsigned, macOS Gatekeeper may show a warning on first open -
right-click the `.pkg` and choose Open, or allow it under System Settings
→ Privacy & Security → "Open Anyway".

**Option 2: one-line terminal install**

```sh
curl -fsSL https://github.com/brianebert/chassis-releases/releases/latest/download/chassis-macos.tar.gz -o /tmp/chassis-macos.tar.gz
tar -xzf /tmp/chassis-macos.tar.gz -C /tmp
/tmp/chassis-macos/install-chassis.sh
```

Either way, this joins your Mac to the shared chassis.engineering/nobody.news network:
an Apple Silicon (arm64) binary, supervised by `launchd`, listening on
port 4919 by default (pass a different port as the first argument). It
grants write access to the network's shared app registry — the same
access every sidecar in the fleet already has. Intel Macs aren't
supported in this build.

To stop it later: `launchctl bootout gui/$(id -u)/engineering.chassis.sidecar-4919`
(a bare `kill` will just get respawned — the installer explains why in its
own comments).
