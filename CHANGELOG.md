# Changelog

All notable changes to Swipe VTT will be documented in this file.

## [1.0.8] - 2026-01-14

### Added
- Daggerheart adversary mobile sheet support
  - Adversary-specific header with HP/Stress display
  - Difficulty and Attack modifier stats
  - Attack section using system.attack ActionField
  - Reaction roll button
  - Damage thresholds row (Minor/Major/Severe)
- Dynamic tab rendering based on actor type
  - PCs: Traits, Loadout, Inventory, Features, Effects, Bio
  - Adversaries: Traits, Features, Effects

### Fixed
- Tab navigation updates correctly when switching between actor types
- Adversary attacks use system.attack instead of weapon items
- Range labels properly localized

## [1.0.7] - 2026-01-13

### Added
- Modular sheet architecture with base classes
- System router for multi-system support
- Daggerheart system support (initial)

### Changed
- D&D 5e sections moved to dedicated directory
- Dev mode support with production safety checks

## [1.0.0] - 2025-12-01

### Added
- Foundry VTT v13 compatibility
- Modular sheet architecture
- Multi-system support framework

## [0.9.1] - 2025-01-10

### Changed
- Improved premium bundle loading reliability
- Optimized module initialization

## [0.9.0] - 2025-01-09

### Added
- Initial public release
- Touch controls for canvas navigation (pan, pinch-zoom)
- Token interaction (tap, double-tap, long-press)
- Mobile device detection with auto-enable
- Portrait/landscape orientation support
- Safari compatibility fixes
- Premium feature framework with Patreon integration

### Premium Features
- Mobile character sheets with bottom drawer UI
- Combat, Inventory, Spellbook, Features, Effects, Biography sections
- Image optimizer for scene backgrounds and tokens
- Mobile chat drawer
- Touch-friendly template placer
