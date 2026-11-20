# Lily architecture

How the three repositories fit together and why. Per-repo detail (tabs, IPC, storage, extensions) is in [Lily-macos's README](https://github.com/Lily-browser/Lily-macos#architecture).

## Layering

```
┌────────────── Lily-macos ──────────────┐   ┌──────────────── Lily-ios ────────────────┐
│ AppKit + SwiftUI shell                 │   │ SwiftUI shell (planned)                  │
│ tabs/windows, sidebar, command bar     │   │ tab switcher, address bar, share sheet   │
│ WKWebExtension runtime, downloads      │   │ iOS extension hosting, Handoff           │
│ injections/*.js, signing, DMG          │   │ App Store / TestFlight packaging         │
└───────────────────┬────────────────────┘   └───────────────────┬──────────────────────┘
                    │  depends on (pinned tag)                   │
                    └──────────────────┬─────────────────────────┘
                                       ▼
                 ┌──────────────────── LilyKit ────────────────────┐
                 │ sealed storage · Keychain key store             │
                 │ history · bookmarks · site settings · drafts    │
                 │ page IPC: envelopes, router, payload schemas    │
                 │ ad-block conversion · migration readers         │
                 │ assistant (Ollama) client · extension audit     │
                 │ URL / privacy helpers          macOS 14+ · iOS 18+│
                 └──────────────────────────────────────────────────┘
```

## Rules of the split

- **LilyKit never imports AppKit, UIKit or SwiftUI.** Windows, views and web views belong to the apps. Platform differences inside the kit are `#if os(macOS)` fences, not copies.
- **Dependency direction is one way**: apps → kit. The kit knows nothing about an app; anything environment-specific (a user agent, a data directory) is passed in.
- **Pinned versions.** Apps pin the kit by exact tag, so a kit change reaches an app only through a reviewed bump. Flow: PR in LilyKit → merge → tag → PR in each app that bumps the pin (with the code that needs it).
- **Same security rules everywhere** (concurrency, logging, Keychain, WebKit message schemas, no process spawning, pinned dependencies), enforced by each repo's `scripts/security-lint.sh` in CI.
- **Tests live with the code**: kit logic is tested in LilyKit (macOS + iOS Simulator build); shell behavior in each app, plus the Mac app's end-to-end self-test.

## What is deliberately not shared (yet)

- The injected page scripts (`injections/`): macOS-only today; they move into the kit as package resources when iOS needs them.
- The WebKit extension runtime: its hosting differs per platform; only manifest/package/audit logic is shared.
- Sync: not built. See [Lily-macos issue #102](https://github.com/Lily-browser/Lily-macos/issues/102).

## Distribution

Mac releases are self-signed DMGs from CI (notarization waits on a paid Apple Developer Program membership). iOS device builds, TestFlight and the App Store need the same membership; simulator builds don't.
