# iPhoneMirror (USB-only)

Mirror and record an **iPhone or iPad screen + audio on Windows over a USB cable**.
Low latency, up to 60 fps, no cloud, no network.

This is a slimmed **USB-only** fork of
[RayrenSX/iPhoneMirror](https://github.com/RayrenSX/iPhoneMirror) (GPL-3.0). All
wireless/AirPlay and auto-update behaviour is turned off — see
[What's different](#whats-different-in-this-fork).

## What it does

- **Wired capture** of an iPhone/iPad screen using Apple's USB screen-capture
  protocol (the same one QuickTime uses). No app is installed on the phone.
- **Audio** (48 kHz) over the same cable.
- **Live preview** (Direct3D 11) and **recording to MP4** (H.264 + AAC).
- **OBS** output via window capture.

## Requirements

- Windows 10/11 x64.
- An iPhone/iPad and a USB cable. Verified on iOS 26.5.2 and iOS 18.7.8;
  newer iOS usually works because the USB protocol is stable.
- **One-time Administrator rights** to install the USB capture driver. After
  that, day-to-day capture does not need admin.

## What's different in this fork

- **No wireless / AirPlay.** The wireless receiver never starts, so the app
  opens **no network ports**. (USB projection modes are unaffected.)
- **No auto-update.** The app never contacts GitHub or downloads updates.
- **Cable only.** No telemetry, no component downloads — nothing leaves the
  machine.

The wireless code still exists in the source but is disabled; it is not shipped
as a working feature.

## Install & use

1. Get a build (see [Building](#building)) and run the setup, or unzip the
   portable build.
2. Open the driver manager and install the USB capture driver (needs admin
   once). Do **not** use Zadig.
3. Connect the iPhone/iPad over USB, unlock it, and tap **Trust This Computer**.
4. Pick the device in the app to preview; use the record button for MP4.

> Not commercially code-signed, so Windows SmartScreen may warn on first run.

## Building

This is a Windows-only app (WPF + native C++), so it is built on Windows.

- **Cloud (no local setup):** push to GitHub and let the `Windows x64 build`
  Actions workflow build and publish the installer artifact. A fast
  `C# quick check` workflow compiles the managed app in ~2 minutes for quick
  iteration.
- **Local:** install Visual Studio 2026 C++ Build Tools, the .NET 10 SDK, and
  Python 3.13, then run `./build.ps1 -Configuration Release`. Add
  `-OmitUxPlayRuntime` to skip the wireless component (no MSYS2 needed).

## License & credit

GPL-3.0, same as upstream. All original work is by
[RayrenSX/iPhoneMirror](https://github.com/RayrenSX/iPhoneMirror); this fork only
disables wireless and auto-update for a USB-only build. The project uses Apple's
private USB protocol (reverse-engineered); future iOS versions may break it.
