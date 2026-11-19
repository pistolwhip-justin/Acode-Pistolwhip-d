# ⚡ Acode — Pistol Whip Edition

&nbsp;&nbsp;![Build](https://img.shields.io/github/actions/workflow/status/pistolwhip-justin/Acode-Pistolwhip-d/release-1.13.6.yml)&nbsp;&nbsp;![Version](https://img.shields.io/badge/version-1.13.6-blue)&nbsp;&nbsp;![License](https://img.shields.io/badge/source%20license-MIT-green)&nbsp;&nbsp;![Android](https://img.shields.io/badge/platform-Android-brightgreen)

Welcome to my customized build of **Acode**, the Android code editor. This repository starts from the complete upstream Acode source and produces a community-built APK with the paid feature set enabled and advertising integration excluded. The goal is straightforward: a capable, no-ad code editor that I can build, inspect, test, and maintain from my own GitHub repository.

This is an independent community build. It is not an official Acode release and is not affiliated with or endorsed by the Acode Foundation or the original authors.

## 🎭 Background & Purpose

Acode is an open-source code editor and web IDE for Android. This edition uses the upstream project's documented `paid` build variant rather than modifying individual Pro feature gates or relying on purchase verification.

### What this edition changes

- 🔓 **Pro features enabled:** the upstream paid package variant sets Acode's Pro feature flag.
- 🚫 **No AdMob integration:** the paid build configuration removes the AdMob and legacy consent plugins.
- 📦 **Independent Android identity:** installs as `com.pistolwhip.acode`, so it can coexist with the official Acode package. The internal Android resource namespace remains `com.foxdebug.acode` for compatibility with upstream Java/plugin sources.
- 🏗️ **Reproducible cloud builds:** GitHub Actions builds the APK from the committed source.
- 🚀 **Versioned releases:** installable APKs are published as GitHub Release assets, not committed to the source tree.

The upstream application is otherwise kept intact. No unrelated editor features or UI redesigns are included in this initial build.

## ✨ Acode Features

The inherited Acode application includes:

- Multi-language code editing with syntax highlighting.
- HTML/CSS/JavaScript editing and browser preview.
- Built-in JavaScript console and terminal.
- SSH, SFTP, and FTP integrations.
- Extensible community plugin support.
- A mobile-friendly editor and file-management workflow.

Feature availability can depend on Android version, plugin support, permissions, and external services.

## 📂 Repository Structure

```text
Acode-Pistolwhip-d/
├── .github/workflows/   # CI and versioned APK release automation
├── src/                 # Acode application source and bundled plugins
├── utils/               # Build configuration and project scripts
├── platforms/           # Generated Android platform project (not committed)
├── codemirror-lsp-client/ # Upstream Git submodule
├── config.xml           # Android package identity and app version
├── package.json         # JavaScript dependencies and build commands
├── license.txt          # Original upstream MIT license notice
└── README.md            # This project guide
```

## 📱 Download & Installation

The current test build is published through the repository's [GitHub Releases](https://github.com/pistolwhip-justin/Acode-Pistolwhip-d/releases).

- **Package:** `com.pistolwhip.acode`
- **Build variant:** upstream `paid`
- **Advertising:** AdMob plugin excluded from this build.
- **Signing:** Android debug signing for sideload testing; this is not a Play Store production build.

Because the package ID is independent, this edition can be installed alongside the official Acode app. Android may ask you to allow installation from the app used to open the APK. Only install builds you trust.

Debug signing is currently intended for first-install testing. A later build produced on a fresh GitHub runner may have a different debug signing key; if Android rejects it as an update, uninstall the prior Pistol Whip test build first. Back up any files stored only inside the app before uninstalling.

## 🏗️ Build From Source

The repository includes the upstream Git submodule. Clone it recursively:

```bash
git clone --recurse-submodules https://github.com/pistolwhip-justin/Acode-Pistolwhip-d.git
cd Acode-Pistolwhip-d
```

### Build requirements

- Node.js 22 or a compatible current LTS release
- pnpm
- JDK 21
- Android SDK / Android build tools
- Git with submodule support

### Build the Pro/no-ad APK

Install dependencies and initialize the Cordova Android project:

```bash
pnpm install
pnpm run setup
```

Build the paid variant in development/debug mode:

```bash
pnpm run build paid dev apk
```

The resulting APK is generated at:

```text
platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

The `paid` argument is intentional: upstream build configuration assigns the paid package identity and removes AdMob/legacy consent plugin integration. The app's runtime Pro flag is enabled for packages that are not the free package identity.

## 🤖 GitHub Actions & Releases

The versioned workflow for this release is:

`.github/workflows/release-1.13.6.yml`

It checks out the exact repository commit and submodule, installs the Android build toolchain, runs the automated test suite, builds the paid APK, verifies its APK signature, calculates SHA-256, and publishes the APK to the matching immutable GitHub Release.

The release tag, version metadata, release title, and APK filename are kept synchronized. Existing releases are not overwritten.

## 🧪 Testing & Known Limitations

- Automated source tests run in GitHub Actions before publication.
- The APK is checked for a valid Android APK signature and its SHA-256 is recorded in the release notes.
- A successful cloud build does **not** prove installation or runtime behavior on every device.
- Physical-device checks still needed: install, first launch, Pro-only functionality, absence of ads, file access, terminal, and plugin behavior.
- This initial release is a debug/sideload build, not a production-signed or Play Store release.
- Android compatibility depends on the upstream Acode requirements and the target device's Android version.

Please report reproducible issues with the Android version, device model, steps, and relevant logs. Do not include private source files, credentials, or personal data in issue reports.

## 📝 Contributing & Development

This repository is a personal derivative of the upstream project. Keep changes focused and preserve upstream functionality wherever possible.

1. Create a feature branch.
2. Make a focused change.
3. Run the relevant checks and tests.
4. Update this README whenever build, usage, feature, compatibility, or release behavior changes.
5. Open a pull request with a clear description and test evidence.

For upstream Acode development guidance, see [Acode's contribution guide](https://github.com/Acode-Foundation/Acode/blob/main/CONTRIBUTING.md).

## 📜 License & Attribution

Acode's original source is distributed under the **MIT License**. The original copyright and permission notice is retained in [`license.txt`](license.txt). This edition preserves that notice and adds its own modifications without replacing upstream attribution.

Third-party dependencies and bundled components may have separate licenses. Review their notices before redistributing modified builds or components.

- Upstream project: [Acode Foundation / Acode](https://github.com/Acode-Foundation/Acode)
- Upstream documentation: [Acode contribution guide](https://github.com/Acode-Foundation/Acode/blob/main/CONTRIBUTING.md)
- License text: [license.txt](license.txt)

## ⚠️ Disclaimer

This is an independently built, unofficial derivative supplied for testing. It is provided as-is. Verify the source and release checksums before installing, and keep backups of important files. The original project and its contributors are acknowledged; this repository does not claim ownership of upstream Acode.

---

Last updated: 2026-11-18
