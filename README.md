# CastSound Desktop

[![Website](https://img.shields.io/badge/website-castsound.app-6C5CE7)](https://castsound.app)
[![Latest release](https://img.shields.io/github/v/release/CastSound/CastSound-Desktop)](https://github.com/CastSound/CastSound-Desktop/releases)
[![Platform](https://img.shields.io/badge/platform-macOS%20%7C%20Linux-lightgrey)](https://castsound.app/download/)

Use your phone as a wireless **speaker**, **microphone**, and **webcam** for your computer.

CastSound Desktop is the companion app for macOS and Linux. Pair it with the
CastSound mobile app on your [Android](https://play.google.com/store/apps/details?id=com.devculi.castsound)
or [iPhone](https://apps.apple.com/app/id6798239521) to stream audio in real
time with low latency over your local network or a USB cable.

## Features

- **Speaker + microphone in one connection** — listen to your computer and
  speak through your phone at the same time.
- **Phone as a webcam** — your computer sees a CastSound camera you can select
  in Zoom, Google Meet, Teams, and OBS (CMIO system extension on macOS,
  v4l2loopback on Linux).
- **Low latency** — built for calls, films, and games; USB tethering gives the
  steadiest link.
- **Auto discovery + QR pairing** — find your computer automatically or scan
  the QR code it shows.
- **Signed auto-updater** — every release is verified with Ed25519 before it is
  installed.

## Install

### macOS

```bash
brew tap castsound/tap
brew trust --cask castsound/tap
brew install --cask castsound
```

Or download the latest `.dmg` from the
[releases page](https://github.com/CastSound/CastSound-Desktop/releases).

The macOS release is signed and notarized with a Developer ID certificate.

### Linux

**Arch Linux (AUR)**

```bash
yay -S castsound-bin
```

**.deb / .rpm**

Grab the package for your distribution from the
[releases page](https://github.com/CastSound/CastSound-Desktop/releases).

**Manual**

Download the tarball for your architecture from the
[releases page](https://github.com/CastSound/CastSound-Desktop/releases), extract
it, and run the `castsound` binary:

```bash
tar xzf CastSound-<version>-linux-x86_64.tar.gz
./castsound
```

## Download

| Platform | Architecture | Download |
|----------|--------------|----------|
| macOS    | Universal (Intel & Apple Silicon) | [`CastSound-<version>-macos-universal.dmg`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-macos-universal.dmg) |
| macOS    | Universal (Intel & Apple Silicon) | [`CastSound-<version>-macos-universal.tar.gz`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-macos-universal.tar.gz) |
| Linux    | x86_64     | [`CastSound-<version>-linux-x86_64.tar.gz`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-linux-x86_64.tar.gz) |
| Linux    | aarch64    | [`CastSound-<version>-linux-aarch64.tar.gz`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-linux-aarch64.tar.gz) |
| Debian / Ubuntu | amd64 | [`castsound_<version>_amd64.deb`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound_<version>_amd64.deb) |
| Fedora / openSUSE | x86_64 | [`castsound-<version>-1.x86_64.rpm`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-<version>-1.x86_64.rpm) |

> **Note:** The in-app auto-updater downloads and verifies the correct archive
> automatically. The files listed above are useful for fresh installs or manual
> updates.

## Quick start

1. Make sure your phone and computer are on the same Wi-Fi network.
2. Open CastSound Desktop.
3. Open the CastSound mobile app and tap **Connect to Desktop**.
4. Scan the QR code shown in the desktop app, or enter the IP address manually.
5. Accept the connection request on both sides.

## Audio driver (macOS)

CastSound Desktop can capture system audio on macOS using the CastSound
Loopback audio driver. The app will prompt you to install the driver when you
select **System Audio** as the capture source. The driver is bundled in the
release archive and is installed with a single click.

## Signature verification

Release archives are signed with Ed25519. Each archive has a matching `.sig`
file that the in-app updater verifies before installation. If you download
manually, you can verify the signature with `openssl`:

```bash
# Download the archive and its signature
curl -LO https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-macos-universal.tar.gz
curl -LO https://github.com/CastSound/CastSound-Desktop/releases/latest/download/CastSound-<version>-macos-universal.tar.gz.sig

# Decode the base64 signature and verify
base64 -d CastSound-<version>-macos-universal.tar.gz.sig > CastSound-<version>-macos-universal.tar.gz.sig.raw
openssl pkeyutl -verify -inkey updater-pubkey.pem -rawin -in CastSound-<version>-macos-universal.tar.gz -sigfile CastSound-<version>-macos-universal.tar.gz.sig.raw
```

The public key ships with the desktop app at
`audio-desktop/assets/updater-pubkey.pem`.

## Auto-updater

CastSound Desktop includes a built-in updater. It checks the latest release on
startup and notifies you when a new version is available. The updater:

1. Queries the GitHub Releases API.
2. Compares the release version with the running version.
3. Downloads the correct archive for your platform.
4. Verifies the Ed25519 signature.
5. Replaces the running app and relaunches it.

## Issues & feedback

Bug reports and feature requests are welcome in
[GitHub Issues](https://github.com/CastSound/CastSound-Desktop/issues). For
setup help, start with the
[setup guides](https://castsound.app/guides/) and the
[FAQ](https://castsound.app/faq/) on the website.

## Learn more

- Website: https://castsound.app
- Download: https://castsound.app/download/
- Support: https://castsound.app/support/
- Terms of Service: https://castsound.app/terms
- Privacy Policy: https://castsound.app/privacy
