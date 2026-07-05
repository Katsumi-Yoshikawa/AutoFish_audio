# AutoFish_backend

AutoFish_backend is a native macOS utility for monitoring loopback/system audio and sending configured keyboard actions to a selected target application. It is designed for workflows where an audible event should trigger a small, repeatable key sequence without manually switching back to the target app.

The app listens to an available audio capture backend, displays realtime volume activity, and can trigger key actions when the realtime volume exceeds a user-defined threshold. It also includes optional timers for periodic actions such as Auto Lure and Auto Log in-out.

## What It Does

- Select a running target application.
- Capture system or loopback audio input, including BlackHole 2ch fallback capture on older macOS versions.
- Monitor realtime volume and trigger when volume crosses the configured threshold.
- Send configured keyboard events directly to the selected target process.
- Configure randomized before-key and between-key delays.
- Configure run duration and cooldown timing.
- Run Auto Lure on an optional interval.
- Run Auto Log in-out with randomized cycle and key interval ranges.
- Record runtime trigger logs, including similarity field, before-key delay, and between-key delay.

## System Requirements

- macOS 11 Big Sur or later.
- Xcode command line tools or Xcode for building from source.
- Accessibility permission for keyboard event delivery.
- Microphone/audio input permission when using a fallback loopback input.
- A loopback audio device such as BlackHole 2ch is recommended for macOS 11 Big Sur and macOS 12 Monterey.

## Quick Start

Build and run the backend-named app:

```bash
./script/build_backend.sh --verify
```

The generated app bundle is created at:

```text
dist/AutoFish_backend.app
```

To copy the generated app to Downloads:

```bash
ditto dist/AutoFish_backend.app ~/Downloads/AutoFish_backend.app
```

## Basic Usage

1. Open AutoFish_backend.
2. Select the target application from the running app list.
3. Configure Int. Key, Fishing Key, key delays, run duration, and cooldown.
4. Select a fallback input device such as BlackHole 2ch if native system audio capture is unavailable.
5. Set a Volume trigger threshold using the same scale as the Realtime and Maximum volume values shown in Realtime Audio Check.
6. Optionally enable Auto Lure or Auto Log in-out.
7. Click Start.
8. Click Pause or Stop when needed. The app also stops automatically after the configured run duration.

See [Usage Guide](docs/USAGE.md) for detailed setup instructions.

## Permissions

AutoFish_backend requires macOS Accessibility permission to send keyboard events. When using BlackHole or another fallback loopback device, macOS may also require microphone/audio input permission because the loopback device is exposed to apps through the audio input permission model.

See [Permissions](docs/PERMISSIONS.md) for details.

## Safety Boundary

AutoFish_backend does not read, inspect, or modify the selected target application's memory, data, settings, or files. It uses public macOS APIs for audio capture and keyboard event delivery.

Keyboard events are synthetic events. Some applications may ignore them, treat them differently from physical keyboard input, or restrict background delivery. AutoFish_backend does not attempt to bypass application security, anti-cheat, anti-bot, or automation detection systems.

See [Limitations](docs/LIMITATIONS.md) before using or modifying the app.

## Development

Run tests:

```bash
env DEVELOPER_DIR=/Applications/Xcode.app/Contents/Developer swift test
```

Build the default app:

```bash
./script/build_and_run.sh --verify
```

Build the backend-named app:

```bash
./script/build_backend.sh --verify
```

See [Development Guide](docs/DEVELOPMENT.md) for project structure and packaging notes.
