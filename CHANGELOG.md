# Changelog

All notable changes to Swipe VTT will be documented in this file.

## [1.10.0]

### Added
- **Standalone mode** for memory-constrained phones (iPhones, low-RAM Android)
  - Lightweight HTML app that bypasses Foundry's client entirely
  - Socket.io connection with session auth and real-time world data sync
  - Full character sheet rendering (combat, inventory, spellbook, features, biography, effects)
  - GM-proxied dice rolling with mobile roll dialog
  - Chat drawer with GM-relayed rendered HTML messages
  - Effects/conditions with status toggling
  - Hit die rolls, short rest, and long rest
  - Group actor Members tab with member summaries
  - Activity use, attack, and damage buttons
  - Premium bundle loading
  - Pause/unpause game and log out
- **Performance mode overlay dialog** for mobile devices
  - Native overlay replaces ApplicationV2 window on phones
  - Standalone as a selectable performance mode tier
  - Player-side mode override with reset button
  - Seamless navigation between standalone ↔ Foundry modes
- Invite URL override setting for VPN/proxy QR code URLs
- Stream view: compendium packs init, sheet config, GM journal sharing

### Fixed
- Species/background showing as raw IDs instead of names
- Item uses display when `value` is null (compute from `max - spent`)
- Activity damage formulas showing `@mod`/`@prof` instead of resolved values
- Save DC not displayed on save-type activities
- Token double-tap for unsupported actor types now opens native sheet
- Chat drawer crash in stream view
- Quick controls showing canvas buttons where no canvas exists
- enrichHTML crashes in standalone mode (try/catch across all sections)

### Changed
- Normalize item/class/feature images to 2.35rem across all systems
- Font variable fallback chain with `--mobile-font-fallback`
- Roll dialog scrollable body with max-height constraint
- Journal sheets fullscreen on mobile
- Rename "Connect Phone" to "Swipe QR Code"
- Deduplicate dice tooltip color/filter rules

## [1.7.4]

### Changed
- Sheet-Only mode now uses Foundry's stream view to reduce module load on iOS

## [1.7.1]

### Added
- Memory diagnostics utility for troubleshooting device performance

## [1.7.0]

### Added
- GM-side user mobile configuration
  - GM can set performance mode per-user from desktop settings
  - Force mode option for users whose devices won't load in default mode
  - Useful for iPhones with strict memory limits on heavy worlds

## [1.6.3]

### Changed
- Disable crlngn-ui floating dock on mobile devices
- Move video button between logout and volume in quick controls

## [1.6.1]

### Added
- Push-to-Talk button above quick controls toggle (touch-hold to broadcast)
- A/V settings button in camera dialog to open Foundry's config

## [1.6.0]

### Added
- Settings cleanup utility for orphaned module settings
- Workaround for Seasons & Stars infinite recursion crash on mobile

### Changed
- Allow GM to load premium via world token on new devices

## [1.5.0]

### Added
- Mobile camera dock enhancements
  - Floating, touch-draggable camera dock on phones (position: fixed, drag to reposition)
  - Camera quick controls dialog with Show/Hide Dock, Hide/Show All, and Speaker Only buttons
  - Speaker-only camera mode: CSS grid stacking with opacity crossfade, GM camera always visible as fallback
  - Speaker-only setting in Swipe VTT Settings under new Camera Views fieldset
  - Navigation arrows in camera controls to browse between camera views
  - Touch-hover simulation for camera view controls (tap to show, tap outside to dismiss)
  - Camera dock starts minimized on mobile devices
  - Camera dock hidden until module finishes applying layout classes
- CameraPopout touch drag support (Foundry popouts use mouse-only drag by default)
- Compatibility with crlngn-ui floating dock (skips conflicting handlers when active)

## [1.4.0]

### Added
- Opened module to all members of Patreon, even free. Rename Premium features to Amethyst Club features

### Fixed
- CSS breakpoints for hiding mobile controls

## [1.3.7]

### Added
- Party Group setting: GM can select a dnd5e Group actor as the party
  - Group members appear in the mobile carousel for all players with LIMITED+ permission
  - Works even without tokens on the current scene
- Group actor mobile sheet with 3 tabs (all free):
  - Members: shows avatar, name, class, AC, HP bar; tap to switch to that character
  - Inventory: editable currency grid, collapsible item categories, containers with contents, use button for consumables, expandable item details
  - Biography: enriched summary and full description
- Wake lock to prevent screen dimming and frequent reloads on mobile
- Improved display of Foundry game settings on mobile screen sizes

## [1.3.5]

### Added
- Quantity editor dialog for inventory items (tap quantity to adjust)
- Safari notification for iOS users about potential compatibility

### Changed
- Assistant GM can now load Amethyst Club features without needing to re-authenticate

## [1.3.2]

### Added
- Connect Phone: QR code dialog for connecting a phone as the same user
  - Scan QR code or copy link to bypass the join screen's greyed-out user restriction
  - Standalone phone-join page with auto-join flow and password prompt
  - "Connect Phone" button injected into User Configuration dialog
  - Auto-shows on desktop load with "Don't show again" user flag
  - Localhost detection uses LAN IP for QR code URL

### Fixed
- Minor refinements to canvas pan handling and hook cleanup

## [1.3.0]

### Added
- Expanded Sheet mode for tablets in canvas-disabled mode (premium)
  - Multi-column layout with 2-5 visible sections based on screen width
  - Responsive column sizing with min/max constraints
- Canvas-disabled background image with vignette overlay
  - Default castle background included, customizable via settings
  - File picker with Browse/Clear in settings
- Sidebar long-press handler for tablets (right-click equivalent)
  - Long-press on sidebar tab buttons triggers pop-out window
- Canvas pan detection: unfreezes canvas when external modules pan the viewport
- Dice So Nice prompt in Aggressive performance mode (optional, no longer automatic)

### Changed
- Desktop mobile mode setting renamed for clarity (`enabledOnDesktop`)
- Performance mode dialog: "Use 1x Resolution" renamed to "Disable Pixel Ratio Resolution"
- Aggressive mode description clarifies Dice So Nice is offered, not forced
- Mobile UI controls now visible in canvas-disabled mode on tablets
- Ability card styling refinements (font sizes, spacing, touch targets)
- Combat section: larger subtab touch targets, normalized font weights
- Condition items: larger min-height, improved active/inactive text colors
- Image popout max-height increased to 95dvh

### Fixed
- Character carousel now works without canvas (reads scene tokens directly)
- Canvas freeze indicator responding to external pan events
- Sheet button focus outline removed on mobile

## [1.2.8]

### Fixed
- Access for Assistant GM now follows the logic of player

## [1.2.7]

### Added
- iOS Automated Animations prompt now shows after Performance Mode selection

### Changed
- Reload prompt now triggers for all performance tab setting changes

### Fixed
- Effects tab condition buttons not visually updating after toggle

## [1.2.6]

### Added
- Safari iOS detection and automatic Dice So Nice optimization
  - Auto-sets DSN to low quality mode for WebGL compatibility
- Collapsible category headers in Combat tab (Weapons, Features, spell levels)
- Item descriptions in Combat tab (shown when item is expanded)
- Item properties in Combat tab (weapon properties, spell school/range/duration, etc.)
- Tap uses count to edit item/spell uses (all tabs)
- Touch-to-mouse adapter for external modules that only support mouse events
- Support for Carolingian Combat Tracker (#combat-popout visibility)

### Fixed
- Performance mode refactored: individual settings are now source of truth
- Canvas freeze indicator not appearing (initialization timing issue)

## [1.2.5] - 2026-01-21

### Added
- Warning when enabling Swipe VTT on desktop

### Changed
- Performance settings can now be saved independently of performance mode
- Image optimizer dialog clarifies that videos are not optimized

### Fixed
- Oversized image in Effects tab of D&D 5e sheet

## [1.2.4] - 2026-01-19

### Added
- Performance Mode dialog with device-based recommendations
- Weighted device tier detection (70% memory, 30% GPU)
- Shortcut to disable canvas entirely
- User overrides for Dice So Nice and Automated Animations
- Reload prompt after changing performance mode
- Container loots in dnd5e sheets

### Changed
- Canvas freeze is now free
- Image optimization is now free
- Fixed Disable Automated Animations / Dice So Nice settings 
- Hide "Enable Mobile Mode on Desktop" setting on mobile to avoid confusion
- Removed duplicate files


## [1.1.0] - 2026-01-16

### Added
- PIXI.Assets aliasing for optimized images on mobile
  - Optimized images now load directly instead of swapping after original loads
  - Prevents large images from being downloaded on mobile devices
- Registry validation on startup (GM only)
  - Removes stale entries for optimized files that no longer exist

## [1.0.16] - 2026-01-15

### Added
- World token system for offline GM premium access
  - Players can access Amethyst Club features when GM is offline using cached world tokens
  - World-scoped cache prevents cross-world cache leakage
  - 7-day token validity with automatic refresh
- Link code authentication for Patreon (alternative to popup auth)
  - 2-minute expiry for security
  - Previous codes invalidated when new one is generated
- Large image notification for GMs
  - Permanent warning when navigating to scenes with unoptimized images
  - Directs GM to Image Optimizer in settings

### Changed
- Removed skip functionality from Image Optimizer dialog
- Improved Premium Auth dialog to work correctly in DEV_MODE
- Localized "Sheet & Chat" fieldset legend

### Fixed
- Duplicate notification prevention for large image warnings
- Race condition in premium bundle loading vs canvasReady hook

## [1.0.8] - 2026-01-14

### Added
- Daggerheart adversary mobile sheet support
  - Adversary-specific header with HP/Stress display
  - Difficulty and Attack modifier stats display
  - Attack section using system.attack ActionField
  - Reaction roll button
  - Damage thresholds row (Minor/Major/Severe)
- Dynamic tab rendering based on actor type
  - PCs show 6 tabs: Traits, Loadout, Inventory, Features, Effects, Bio
  - Adversaries show 3 tabs: Traits, Features, Effects

### Fixed
- Tab navigation now properly updates when switching between actor types in carousel
- Adversary attacks now correctly use system.attack instead of weapon items
- Range labels properly localized using CONFIG.DH.GENERAL.range

## [1.0.7] - 2026-01-13

### Added
- Modular sheet architecture with base classes
- System router for multi-system support
- D&D 5e sections moved to dedicated directory
- Daggerheart system support (initial)

### Changed
- Refactored sheet architecture for better extensibility
- Dev mode support with production safety checks

## [1.0.3] - Previous

### Added
- Initial modular sheet architecture
- Base classes for drawer and sections

## [1.0.0] - Initial Release

### Added
- Mobile-friendly interface for Foundry VTT
- Touch controls and gesture recognition
- Mobile-optimized character sheets
- Pinch-zoom and pan gestures on canvas
- Token interaction via touch (tap, double-tap, long-press)
- Bottom drawer UI with avatar carousel
- D&D 5e character sheet support
- Amethyst Club features system with Patreon integration
- Socketlib integration for GM-player bundle sharing
