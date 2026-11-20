# Lily

A native, privacy-first browser for Apple platforms. Pure Swift and SwiftUI over WebKit: vertical tabs, spaces with separate logins, split view, a command bar, ad blocking, local AI through Ollama, and almost nothing running while you're idle. No account, no analytics, no sync server.

| Repository | What | Status |
|---|---|---|
| [**Lily-macos**](https://github.com/Lily-browser/Lily-macos) | The Mac app: AppKit/SwiftUI shell, WebKit extension runtime, signing and DMG releases | 0.4 — usable, [releases](https://github.com/Lily-browser/Lily-macos/releases) |
| [**Lily-ios**](https://github.com/Lily-browser/Lily-ios) | The iPhone/iPad app | planned — rules and plan only |
| [**LilyKit**](https://github.com/Lily-browser/LilyKit) | Platform-neutral Swift package shared by both apps (storage, IPC, ad-block, migration, assistant client, extension logic) | extracted, pre-0.1 |

How the pieces fit together: [ARCHITECTURE.md](https://github.com/Lily-browser/.github/blob/main/ARCHITECTURE.md). Everything is GPL-3.0-only. Questions and ideas go to [Lily-macos Discussions](https://github.com/Lily-browser/Lily-macos/discussions); security reports are private (see each repo's Security tab).

See also [ARCHITECTURE.md](../ARCHITECTURE.md) and [DESIGN.md](../DESIGN.md) (how Lily follows Apple's Human Interface Guidelines and where it stays itself).
