# StrictFox

StrictFox is a hardened `user.js` configuration for Mozilla Firefox. It is designed to maximize privacy, security, and anti-fingerprinting while remaining practical for daily use.

This project is inspired by the research and structure of the [Arkenfox project](https://github.com/arkenfox/user.js). The classic syntax-checking markers are retained as a nod to their foundational work, but the preferences are independently curated and maintained.

## Prerequisites

This configuration works best as part of a layered privacy setup. For optimal protection, it should be used alongside:

1. **Content Filtering**: [uBlock Origin](https://addons.mozilla.org/en-US/firefox/addon/ublock-origin/) for efficient, DOM-level tracker and ad blocking.
2. **Secure DNS**: A privacy-focused, non-logging DNS provider with threat blocking (e.g., [Quad9](https://quad9.net/)), as configured in the [Arch Linux Installation Guide](https://github.com/ciphralab/archlinux-installation-guide).

## Installation

1. Download the [user.js](user.js) file from this repository.
2. Locate your active Firefox profile directory:
   - Open Firefox and navigate to `about:support`.
   - Find the "Profile Folder" (or "Profile Directory") entry and click "Open Folder" (or "Show in Finder" on macOS).
3. Place the `user.js` file directly into this directory. If a `user.js` file already exists, back it up before overwriting or merge the configurations manually.
4. Restart Firefox to apply the preferences.

**Verification**: To confirm the file loaded correctly, navigate to `about:config` and search for `_user.js.parrot`. The value should read:

`SUCCESS: No no he's not dead, he's, he's restin'!`

## Configuration Overview

The configuration enforces the following controls:

- **Telemetry Removal**: Disables Mozilla telemetry, crash reporting, studies, and sponsored content.
- **Anti-Fingerprinting**: Enables `privacy.resistFingerprinting` (RFP), spoofs the locale to English, and restricts window dimensions to blend in with standard user profiles.
- **Network Hardening**: Disables DNS prefetching, speculative connections, and WebRTC IP leakage. Enforces HTTPS-Only mode globally.
- **Disk Avoidance**: Disables disk caching and forces media caching into memory to prevent local data retention.
- **Shutdown Sanitization**: Automatically clears history, cache, cookies, and form data on exit to prevent local data retention and session persistence.
- **Attack Surface Reduction**: Disables WebGL, WebGPU, asm.js, and DRM (EME).
- **Baseline Security**: Retains Google Safe Browsing for practical malware and phishing protection.

## Operational Trade-offs

Because of these strict controls, some web features will not work out of the box. This is an intentional trade-off for privacy:

- **Media Streaming**: DRM-protected services (Netflix, Spotify, etc.) will not work, as EME is disabled.
- **Advanced Web Apps**: Sites relying on WebGL, WebGPU, or precise hardware timing may fail to render.
- **Credential Management**: Built-in password and form autofill are disabled. Use a dedicated password manager (e.g., Bitwarden, KeePassXC).
- **RFP Quirks**: `privacy.resistFingerprinting` may cause minor layout issues on sites that rely on dynamic window sizing or specific timezone/clipboard APIs.

## Maintenance

Firefox frequently updates and changes default preferences. To maintain this security posture:
1. Periodically check this repository for `user.js` updates.
2. Review `about:config` after major Firefox updates to ensure no new tracking features have been enabled by default.

## License

This project is licensed under the [MIT License](LICENSE).
