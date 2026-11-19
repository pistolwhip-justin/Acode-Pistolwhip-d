# ⚡ Acode — Pistol Whip Edition

&nbsp;&nbsp;![Build Status](https://img.shields.io/github/actions/workflow/status/pistolwhip-justin/Acode-Pistolwhip-d/release-1.13.6.yml)&nbsp;&nbsp;&nbsp;&nbsp;![License](https://img.shields.io/badge/license-MIT-green.svg)&nbsp;&nbsp;&nbsp;&nbsp;![Android](https://img.shields.io/badge/platform-Android-brightgreen.svg)&nbsp;&nbsp;&nbsp;&nbsp;![Version](https://img.shields.io/badge/version-1.13.6-blue.svg)

Welcome to my Android code-editor side quest! This is my customized build of **Acode**, starting from the complete upstream source and turning it into a no-ad, Pro-enabled editor that I can build, inspect, test, and maintain through GitHub.

The goal is pretty simple: keep the useful Acode experience, ditch the advertising integration and paid-feature gate, and keep the whole process transparent. No mystery APKs, no modified third-party downloads, and no guessing about what went into a build.

## 🎭 Background

Acode is an open-source code editor and web IDE for Android. It's a solid starting point, but I want an edition I can control and maintain myself.

This repository is an independent community build—not an official Acode release and not affiliated with or endorsed by the Acode Foundation or the original authors.

### Why this edition?

- 🔓 **Pro features enabled** — uses Acode's documented `paid` build variant instead of patching individual feature gates.
- 🚫 **AdMob integration excluded** — the paid build configuration removes the AdMob and legacy consent plugins.
- 📦 **Own Android package ID** — installs as `com.pistolwhip.acode`, so it can live alongside the official Acode app.
- 🏗️ **Build it in the cloud** — GitHub Actions builds from committed source with a documented Android toolchain.
- 🚀 **Real releases** — the APK lives on its versioned GitHub Release, not buried in the source tree.

## 🌌 What's Included?

The inherited Acode application brings along:

- Multi-language code editing and syntax highlighting.
- HTML, CSS, and JavaScript editing with browser preview.
- Built-in JavaScript console and terminal.
- SSH, SFTP, and FTP integrations.
- Community plugin support.
- Mobile-friendly file management and editor workflows.

Feature availability can still depend on Android version, permissions, plugins, and external services.

## 📂 Repository Structure

```text
Acode-Pistolwhip-d/
├── .github/workflows/     # Versioned APK release + release export automation
├── src/                   # Acode application source and bundled plugins
├── utils/                 # Build configuration and project scripts
├── codemirror-lsp-client/ # Upstream Git submodule
├── config.xml             # Android package identity and app version
├── package.json           # JavaScript dependencies and build commands
├── license.txt            # Original upstream MIT license notice
└── README.md              # This project guide
```

## ⚙️ How to Use This Build

### Download

The current test build is available from the [GitHub Releases page](https://github.com/pistolwhip-justin/Acode-Pistolwhip-d/releases).

- **Version:** 1.13.6
- **Android package:** `com.pistolwhip.acode`
- **Build variant:** `paid` (Pro features enabled)
- **Advertising integration:** AdMob and legacy consent plugin integration excluded.
- **Signing:** Android debug signing for sideload testing—not a Play Store production build.

Because this edition has its own package ID, it can be installed alongside the official Acode app. Android may ask you to allow installation from the app used to open the APK.

**A note about future updates:** GitHub-hosted debug builds use the runner's debug signing identity. If a later build is rejected as an update, uninstall the previous Pistol Whip test build and install the new one. Back up any files stored only inside the app before uninstalling.

### Build it yourself

Clone the repository with its submodule:

```bash
git clone --recurse-submodules https://github.com/pistolwhip-justin/Acode-Pistolwhip-d.git
cd Acode-Pistolwhip-d
```

**Build requirements**

- Node.js 22
- pnpm 10
- JDK 21
- Android SDK, including Android 36 platform and build tools 36.0.0
- Git with submodule support

**Install dependencies and initialize Cordova**

```bash
pnpm run setup
```

**Run checks**

```bash
pnpm run test
pnpm run typecheck
```

**Build the Pro/no-ad APK**

```bash
pnpm run build paid dev apk
```

The generated debug APK is created at:

```text
platforms/android/app/build/outputs/apk/debug/app-debug.apk
```

The `paid` argument is deliberate: upstream build configuration assigns the paid package identity and excludes AdMob integration. Acode's runtime Pro flag is enabled for packages that are not the free package identity.

## 🤖 GitHub Actions & Releases

Each version gets its own release workflow. The current workflow is:

`.github/workflows/release-1.13.6.yml`

It checks the release/tag state, checks out the exact source and submodule, configures the Java/Android/Node toolchain, runs tests and type checks, builds the paid APK, verifies the package ID and APK signature, and publishes the APK as a GitHub Release asset.

The release guard is intentionally strict: an existing complete release is left alone; an incomplete or inconsistent release fails safely instead of being overwritten.

The helper workflow `.github/workflows/export-release-apk.yml` retrieves the already-published APK, verifies its SHA-256, and exports a short-lived Actions artifact for in-chat file delivery. The GitHub Release remains the canonical distribution location.

## 🧪 Testing & Known Limitations

- ✅ Automated tests passed for the 1.13.6 source.
- ✅ Type checks passed.
- ✅ APK signature verified.
- ✅ APK package ID verified as `com.pistolwhip.acode`.
- ✅ Published release asset checksum verified.
- ⏳ Physical-device installation and runtime checks still need to be completed.

A successful cloud build does **not** prove the app installs or behaves correctly on every device. The remaining device checks include first launch, Pro-only functionality, absence of ads, file access, terminal behavior, and plugin behavior.

Please report reproducible issues with the Android version, device model, steps, and relevant logs. Don't include private source files, credentials, or personal data in issue reports.

## 📝 Contributing

This is a personal derivative of the upstream project. Keep changes focused, preserve upstream functionality wherever possible, and don't add unrelated features just because they're shiny.

1. Fork or clone the repository.
2. Create a feature branch (`git checkout -b feature/improvement`).
3. Make a focused change.
4. Run the relevant checks and tests.
5. Update this README when build, usage, feature, compatibility, or release behavior changes.
6. Open a pull request with a clear description and test evidence.

For upstream development guidance, see [Acode's contribution guide](https://github.com/Acode-Foundation/Acode/blob/main/CONTRIBUTING.md).

## 📜 License

Acode's original source is distributed under the **MIT License**. The original copyright and permission notice is retained in [`license.txt`](license.txt). This edition preserves upstream attribution and adds its own modifications without replacing the original notice.

Third-party dependencies and bundled components may have separate licenses. Review their notices before redistributing modified builds or components.

- Upstream: [Acode Foundation / Acode](https://github.com/Acode-Foundation/Acode)
- Contribution guide: [Acode contribution guide](https://github.com/Acode-Foundation/Acode/blob/main/CONTRIBUTING.md)
- License text: [license.txt](license.txt)

## ⚠️ Disclaimer

This is an independently built, unofficial derivative supplied for testing. It is provided as-is. Verify the source and release checksums before installing, and keep backups of important files. The original project and its contributors are acknowledged; this repository does not claim ownership of upstream Acode.

## 🙏 Acknowledgments

- The Acode Foundation and the original Acode contributors.
- The open-source maintainers of the libraries and plugins used by the project.
- The Android and Cordova communities that make a cloud-built Android workflow possible.

---

Last updated: 2026-11-18
