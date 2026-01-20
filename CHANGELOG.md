# Changelog

All notable changes to Swipe VTT will be documented in this file.

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
  - Players can access premium features when GM is offline using cached world tokens
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
- Premium features system with Patreon integration
- Socketlib integration for GM-player bundle sharing
