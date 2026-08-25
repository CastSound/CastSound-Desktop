# CastSound Desktop

Turn your phone into a wireless microphone and speaker for your computer.

CastSound Desktop is the receiver app for macOS, Linux, and Windows. Pair it
with the CastSound mobile app to stream audio between your devices with low
latency over your local network.

![CastSound Desktop screenshot](screenshot.png)

## Download

Pick the build for your platform from the latest release.

| Platform | Architecture | Download |
|----------|--------------|----------|
| macOS    | Universal (Intel & Apple Silicon) | [`castsound-macos-universal.tar.gz`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-macos-universal.tar.gz) |
| Linux    | x86_64     | [`castsound-linux-x86_64.tar.gz`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-linux-x86_64.tar.gz) |
| Windows  | x86_64     | [`castsound-windows-x86_64.zip`](https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-windows-x86_64.zip) |

> **Note:** The in-app auto-updater downloads and verifies these same archives
> automatically. The files listed above are useful for fresh installs or manual
> updates.

## Quick start

### macOS

1. Download `castsound-macos-universal.tar.gz`.
2. Extract the archive.
3. Move `CastSound.app` to your `Applications` folder.
4. Launch CastSound from Launchpad or Finder.

On first run you may need to right-click the app and choose **Open** because
the release is signed with an ad-hoc signature.

### Linux

1. Download `castsound-linux-x86_64.tar.gz`.
2. Extract the archive:
   ```bash
   tar xzf castsound-linux-x86_64.tar.gz
   ```
3. Move the binaries to a directory on your `PATH`:
   ```bash
   sudo install -m 755 castsound castsound-cli /usr/local/bin/
   ```
4. Run `castsound`.

### Windows

1. Download `castsound-windows-x86_64.zip`.
2. Extract the zip file.
3. Move `castsound.exe` and `castsound-cli.exe` to a folder of your choice.
4. Double-click `castsound.exe` to start the app.

## Pairing with your phone

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
curl -LO https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-macos-universal.tar.gz
curl -LO https://github.com/CastSound/CastSound-Desktop/releases/latest/download/castsound-macos-universal.tar.gz.sig

# Decode the base64 signature and verify
base64 -d castsound-macos-universal.tar.gz.sig > castsound-macos-universal.tar.gz.sig.raw
openssl pkeyutl -verify -inkey updater-pubkey.pem -rawin -in castsound-macos-universal.tar.gz -sigfile castsound-macos-universal.tar.gz.sig.raw
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
  universal binary support. Run `scripts/build/macos.sh` for a full release
  build.
- **Linux:** Install ALSA/PipeWire development packages. See
  `.github/workflows/ci.yml` for the exact Ubuntu dependencies.
- **Windows:** Visual Studio Build Tools with the Windows SDK.

## Documentation

- [Architecture overview](https://github.com/CastSound/CastSound-Desktop/blob/main/docs/architecture.md)
- [Protocol details](https://github.com/CastSound/CastSound-Desktop/blob/main/docs/protocol.md)
- [Testing guide](https://github.com/CastSound/CastSound-Desktop/blob/main/docs/testing.md)

