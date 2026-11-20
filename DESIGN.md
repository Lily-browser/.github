# Lily design language

Lily should feel like it was made by Apple's neighbors: it follows Apple's
[Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines) so it behaves the way
Apple platform users expect, and keeps a few signature touches so it is recognizably Lily.

## The rule

**Platform first, Lily second.** Use system components, system type, system materials and system behavior.
Add Lily only where it carries identity without costing accessibility or familiarity.

## What follows Apple

| Area | How |
|---|---|
| Type | System font and text styles (Dynamic Type). No fixed point sizes for text. |
| Color | Semantic system colors for text, fills and separators; both light and dark are designed together. |
| Materials | System materials for chrome. On macOS/iOS 26 and later, floating chrome is Liquid Glass (system controls get it automatically; custom chrome uses `glassEffect` behind an availability check with a material fallback). Glass is for chrome, never for page content. |
| Targets | 44 × 44 pt minimum on iOS; native control sizes on the Mac. |
| Accessibility | Every control has a label; tappable views are real buttons with selected/disabled state; Reduce Motion, Reduce Transparency and Increase Contrast are honored; color is never the only signal. |
| Navigation | Sheets for modal tasks, standard Settings, the menu bar and keyboard shortcuts on the Mac, context menus for secondary actions, edge-swipe and gestures on iOS. |
| Privacy | Plain language, explicit confirmation for destructive actions, nothing leaves the device without the user knowing. |

## What stays Lily

- **Indigo accent** (`#5E5CE6`, the app icon's color), user-changeable, shared by both apps.
- **Spaces**: each has a symbol and a color that washes the sidebar (Mac) or the backdrop (iOS) behind the page.
- **The page as a rounded card** floating on that tint, so content is the focus and the chrome recedes.
- **A command bar** instead of a toolbar full of buttons: one floating field for addresses, searches and tabs.
- **The leaf** and the quiet, private tone of the copy.
- Optional paper grain and sidebar tint on the Mac (off under Increase Contrast).

## Per-platform notes

- **Mac:** sidebar of tabs, pinned tiles, split view, Little Lily, command bar centered over the page. Standard window
  and menu bar behavior; custom views must still expose accessibility labels and traits.
- **iPhone:** one hand, one task. Bottom bar (back, address pill, tabs, new tab), card-grid tab overview as a sheet,
  space switcher as a floating capsule. Settings are short on purpose.
- **iPad (planned):** sidebar like the Mac in regular width, bottom bar only in compact width, keyboard shortcuts.

## Status (see each repo's PRs for details)

- iOS: HIG pass done (Liquid Glass with fallback, Dynamic Type, VoiceOver, 44 pt targets, Reduce Motion).
- macOS: VoiceOver labels and traits added; Increase Contrast turns off decorative tint and grain.
- **Open:** iPad and landscape layouts; measured contrast for the colored site badges and tinted sidebars; adopting
  Liquid Glass for the Mac's custom floating surfaces (command bar) behind a macOS 26 check; VoiceOver pass on devices;
  localization and right-to-left review.
