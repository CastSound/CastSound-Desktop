# CastSound Desktop

Turn your phone into a wireless microphone and speaker for your computer.

CastSound Desktop is the receiver app for macOS and Linux. Pair it with the
CastSound mobile app to stream audio between your devices with low latency over
your local network.

## Install

### macOS

```bash
brew install --cask castsound
```

Or download the latest `.dmg` or `.tar.gz` from the
[releases page](https://github.com/CastSound/CastSound-Desktop/releases).

The macOS release is signed and notarized with a Developer ID certificate.

### Linux

**Flatpak (recommended)**

```bash
flatpak install flathub com.devculi.castsound
```

**Arch Linux (AUR)**

```bash
yay -S castsound-bin
```

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

The public key is embedded in the desktop app at
`audio-desktop/assets/updater-pubkey.pem` in the source repository.

## Auto-updater

CastSound Desktop includes a built-in updater. It checks the latest release on
startup and notifies you when a new version is available. The updater:

1. Queries the GitHub Releases API.
2. Compares the release version with the running version.
3. Downloads the correct archive for your platform.
4. Verifies the Ed25519 signature.
5. Replaces the running app and relaunches it.

## Building from source

The desktop app is a Rust workspace. You need the latest stable Rust toolchain
and platform dependencies.

```bash
git clone https://github.com/CastSound/CastSound-Desktop.git
cd CastSound-Desktop
cargo build --release -p audio-desktop
```

Platform-specific build notes:

- **macOS:** Xcode Command Line Tools are required for the loopback driver and
  universal binary support.
- **Linux:** Install ALSA/PipeWire development packages.
- **Windows:** Visual Studio Build Tools with the Windows SDK.

## Learn more

- Website: https://castsound.app
- Terms of Service: https://castsound.app/terms
- Privacy Policy: https://castsound.app/privacy
