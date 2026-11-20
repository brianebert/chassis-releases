# chassis releases

Prebuilt macOS installer releases for [chassis](https://chassis.engineering) —
a small P2P document-and-payments sidecar that powers the
chassis.engineering/nobody.news network. Source lives in a private repo;
this repo holds only built, downloadable release artifacts.

## Install

### Option 1: double-click

Download [chassis-installer.pkg](https://github.com/brianebert/chassis-releases/releases/latest/download/chassis-installer.pkg)
and open it. It installs into your own home folder, with no admin
password. Opening a newer one later updates an existing install in place
and restarts it; your data is kept.

### Option 2: terminal

```sh
curl -fsSL https://github.com/brianebert/chassis-releases/releases/latest/download/chassis-macos.tar.gz -o /tmp/chassis-macos.tar.gz
tar -xzf /tmp/chassis-macos.tar.gz -C /tmp
/tmp/chassis-macos/install-chassis.sh
```

This joins your Mac to the shared chassis.engineering/nobody.news network:
an Apple Silicon (arm64) binary, supervised by `launchd`, listening on
port 4919 by default (pass a different port as the first argument). It
grants write access to the network's shared app registry — the same
access every sidecar in the fleet already has. Intel Macs aren't
supported in this build.

To stop it later: `launchctl bootout gui/$(id -u)/engineering.chassis.sidecar-4919`
(a bare `kill` will just get respawned — the installer explains why in its
own comments).

## Updates and signatures

Release binaries are signed with a Developer ID certificate (Team ID
`8LZB8WN288`) and notarized by Apple; the .pkg is signed, notarized and
stapled. Check a binary with `codesign -dv bottom_up`.

To update a terminal install: `~/Library/Application\ Support/chassis/install-chassis.sh --update`
(`--check-update` only reports). From v8 on, `--update` refuses a binary
that isn't signed by that team. An install on v7 or earlier runs its old
updater once, so that one step isn't checked.
