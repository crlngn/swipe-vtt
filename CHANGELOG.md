# Changelog

All notable changes to Swipe VTT will be documented in this file.

## [1.21.1]

### Fixed
- **`Token#detectionModes` shape change on Foundry V14** — V14 switched detection modes from an `ArrayField` to a `TypedObjectField` keyed by mode id, so `(t.detectionModes ?? []).map(...)` threw `.map is not a function` when switching levels. Added `TokenCompat.getDetectionModes` to normalize the two shapes; applied to the standalone scene-packet builder, the standalone `createToken` broadcast, and the MiniCanvas sight-range / visibility computations.
- **Actor cache build threw on dnd5e 5.3+** — `details.race` and `details.background` became getter-only in dnd5e 5.3, breaking the standalone actor-cache builder. Now version-gated: dnd5e ≥ 5.3 shallow-clones `details` before mutating, older versions keep the direct-assignment path.

## [1.21.0]

### Added
- **Foundry V14 compatibility for scene image features** — V14 moved `Scene#background` and `Scene#foreground` onto an embedded `Level` document and emits a deprecation warning every time the legacy accessors are read. Image optimization, the optimized-image swap-in, and memory diagnostics now use a version-aware adapter (`SceneCompat`) that reads from `scene.firstLevel` on V14+ and the legacy fields on V13. Single-level scenes behave identically across versions.
- **Multi-level scene support for image optimization and memory tally on V14** — multi-level scenes (a V14-only feature) now have every Level's background/foreground analyzed by the optimizer dialog and counted in the texture-memory estimate. Per-level entries are labeled with the Level name (e.g., "Background (Upper Floor)") to disambiguate.

## [1.20.1]

### Fixed
- **Assistant GMs couldn't load premium bundles** — `socketlib.executeAsGM` short-circuits to a local handler when the caller's `isGM` flag is true, which in V13 includes Assistant GMs. The Assistant would dispatch the bundle request to themselves, fail the patron check, and end up with premium disabled. Bundle requests (and version-broadcast re-fetches) now route explicitly to the active primary GM.

## [1.20.0]

### Added
- **Wall geometry on Simplified Token Map** — a 60ft circular reveal around the player's selected (or last-dragged) token shows nearby wall lines, with a feathered/gradient outer edge. Closed and locked doors render distinct from solid walls; open doors render dashed.
- **Live door state propagation** — toggling a door open/closed/locked on the GM canvas updates the simplified map for connected players in real time (via `updateWall` hook in-Foundry, and a new socket broadcast for Standalone clients).
- **GM setting: "Show Walls on Simplified Token Map"** — world-scope toggle (default ON) under the GM-only section of the Swipe VTT settings dialog. Disable for theatre-of-the-mind scenes.
- **Secret door privacy** — secret doors (`door=SECRET`) and non-blocking walls (`move=NONE`) are filtered server-side before reaching player clients.
- **GM-offline blocks player movement** — if no GM is connected, MiniCanvas drags are rejected client-side with a "GM must be online" notification (in-Foundry and Standalone).

### Fixed
- **SocketUtil missed `socketlib.ready` hook** — on player clients where socketlib finished initialization before our module, `Hooks.once` never fired and `SocketUtil.socket` stayed null. Visibility relay, premium bundle requests, and the new movement validator silently no-op'd. Now registers synchronously when socketlib is already loaded.
- **Simplified Token Map selection wiped on token refresh** — `createTokens()` now snapshots and restores the previous selection and target state, so server-side token updates, drags, or the periodic sync no longer clear the player's active selection.
- **Wall radius followed wrong token after drag** — the dragged token now becomes the active selection at drop time, so the 60ft wall reveal centers on the last-moved token, not the player's main character.

## [1.19.2]

### Added
- **MiniCanvas wall collision check on player drags** — players can no longer drag tokens through scene walls on the Simplified Token Map. Drag commits are validated by the GM client via socketlib using Foundry's polygon backend (`CONFIG.Canvas.polygonBackends.move.testCollision`); blocked moves snap back with a notification. Honors closed/locked doors and one-way walls; open doors and `move=NONE` walls allow passage.

### Fixed
- **GM premium cache stale mid-session** — refresh the GM's premium cache during the session so players get the current bundles after the GM reconnects or refreshes Patreon status.

## [1.19.1]

### Changed
- **GM premium relay when Swipe disabled** — GMs with "Enable Swipe in this client" off now run the premium socket + session init only, so players can still validate premium through them. No mobile UI is loaded on the GM's client.

### Fixed
- **World-token fallback for fresh installs** — players whose GM is online but unresponsive (or returns a generic error) now fall back to the world token after the cache, closing the gap on fresh installs.

## [1.19.0]

### Added
- Toggle to disable Swipe in a specific client (per-user)
- GM / Assistant GM users now appear in the Swipe mode configuration in Settings
- QR code link for all players (shared by the GM)
- Touch-drag and window drag handler improvements

## [1.18.2]

### Fixed
- Macro hotbar drawer z-index when the sheet carousel is open
- Macro slot image expanding on long press

### Changed
- Macro hotbar button is now visible by default (`hideMacroButton` default: false)

## [1.18.1]

### Added
- **Inventory: Attune/Unattune toggle** — items with attunement show an attune button in expanded details
- **Inventory: Delete item** — remove button with confirmation dialog in expanded item details
- **Inventory: Add Item** — button to add items from the compendium browser (filtered to inventory types)
- **Macro hotbar drawer** — mobile-friendly macro hotbar with grid layout matching Foundry core style
  - Toggle button in button stack (hidden by default, enable in Settings > Controls)
  - Page navigation between hotbar pages
  - Long-press context menu: add, edit, remove macros
  - Macro search dialog for adding from world macros or compendium packs
  - Drag-and-drop to reorder or swap macro slots
  - Drag handle to dismiss drawer
- Fade mask on scrollable item descriptions in expanded details

### Fixed
- **TextureLoader deprecation** — use `foundry.canvas.TextureLoader` (Foundry V13+)
- **Senses deprecation** — read from `senses.ranges.*` for dnd5e 5.3+ compatibility
- **Window drag position sync** — close button no longer snaps window to original position after dragging
- **Dice bar positioning** — always appears above the dice button regardless of other buttons
- Activity name overflow in inventory — truncated with ellipsis
- Drawer handle touch targets increased for easier interaction

## [1.17.4]

### Added
- Auto-optimization for scenes via setting and improved optimizer prompt dialog
- Scene image check to warn when images exceed device max texture size
- Default scene image size threshold changed to 2048px

### Fixed
- Clean up premium loader notifications (use LogUtil, mobile-only reporting)

## [1.17.0]

### Added
- **MiniCanvas** — lightweight grid + token view for noCanvas mode
  - MiniCanvas enable/allow settings with opt-in prompt
  - MiniCanvas support for standalone mode
- Support delete templates via socket in standalone mode
- Send target token IDs with standalone roll requests

### Fixed
- Guard preventDefault with cancelable check in touch handlers
- Standalone MiniCanvas token undo

## [1.16.3 – 1.16.8]

### Fixed
- Premium loader improvements and debug messages
- Player bundle caching: cache check before patron status check
- Patreon token invalidation fix
- Patreon re-authentication prompt
- Patreon connection window showing connected without valid session token

## [1.16.0]

### Added
- **Controls settings** (General tab) with two new options:
  - **Hide Quick Controls** — hides the floating quick controls toolbar; on tablets also hides the settings button, on phones the settings button remains since Foundry's sidebar is hidden
  - **Hide Avatar Carousel** — hides the character avatar carousel; sheets can still be opened by double-tapping tokens
  - When quick controls are visible, Foundry's `#players` list is hidden on desktop to avoid overlap
  - Controls fieldset visible on desktop too with a note that settings apply to touch devices only

### Fixed
- `/stream` view no longer modified by Swipe VTT — Foundry's native stream view works as intended

### Removed
- Stream mode initialization (streamReady hook, background override, stream CSS, /stream redirect logic)

## [1.15.0]

### Added
- Player premium: cache-first fallback, version-based cache invalidation
- PF2e spellbook search

### Fixed
- Image optimizer button fixes

## [1.14.0]

### Added
- PF2e spellbook: signature spells, spontaneous casting, variable actions, rank fixes
- Collapsible card content in chat, chat drawer sizing improvements
- Memory diagnostics improvements
- Tools filter for standalone

### Fixed
- Tool rolls and standalone prepared data
- Reload loop fix

## [1.13.0]

### Fixed
- Scope mobile CSS rules to `body.swipe-vtt` to prevent desktop leakage
- GM-offline warnings: track user active state, fix notification visibility
- Roll dialog mode info font sizes

## [1.12.2]

### Added
- GM-offline warnings for standalone rolls, edits, and actions

### Fixed
- Chat toggle button z-index above chat drawer
- Settings checkbox color

## [1.12.1]

### Added
- Pinch-to-zoom for application windows with header touch handling
- Journal quick control, dynamic z-index for drawers
- Blade Runner chat styling

### Changed
- Clarify image optimizer descriptions to reassure desktop scenes are unaffected

## [1.12.0]

### Added
- PF2e NPC sheet: shield, initiative, traits, notes; hide feats/crafting
- PF2e inventory: native coin API, editable qty for contained items
- PF2e sheet: crafting, effects, feats, inventory, spellbook sections + roll dialog setting
- Gate mobile sheets on `enableMobileSheets` setting with fallback carousel

### Changed
- Sheet-only mode stays on `/game` with noCanvas instead of redirecting to `/stream`
- Gate standalone mode to supported systems only (dnd5e)

### Fixed
- Window header tap and position jump on mobile
- Temp Max row hidden in HP dialog for systems without tempmax (PF2e)
- Image optimizer dialog not showing scene analysis on first open

## [1.10.1]

### Added
- **Generic MobileTemplatePlacer** for all systems (PF2e, Daggerheart, etc.)
  - Template previews from any system are now touch-draggable on mobile
  - Uses PIXI childAdded detection on canvas.templates.preview
  - Initial position centers on user's token or viewport center
  - Proper system cleanup via synthetic rightdown to terminate system placement flows
- Generic system CSS overrides for PF2e actor sheets on mobile

### Fixed
- Mobile application dialog min-width and max-width sizing
- Settings user names truncation using max-width instead of white-space

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
