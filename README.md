# Swipe VTT

A mobile-friendly interface for [Foundry VTT](https://foundryvtt.com/) with touch controls, optimized character sheets, and performance enhancements for phones and tablets.

## Features

### Free Features
- **Touch Controls** - Pan and pinch-zoom navigation on the canvas
- **Token Interaction** - Tap to select, double-tap to open sheets, long-press for HUD
- **Mobile Detection** - Automatically enables on mobile devices
- **Portrait/Landscape Support** - Adapts UI to device orientation
- **Safari Compatibility** - Fixes for iOS Safari quirks

### Premium Features
Premium features require a [Patreon](https://www.patreon.com/carolingian) subscription:

- **Mobile Character Sheets** - Bottom drawer UI with swipeable avatar carousel
- **Combat Section** - Quick access to attacks, saves, and ability checks
- **Inventory Management** - Touch-optimized item lists with quantity controls
- **Spellbook** - Spell slots, preparation, and casting interface
- **Image Optimizer** - Compress scene backgrounds and tokens for faster loading
- **Chat Drawer** - Slide-out chat panel optimized for mobile
- **Template Placer** - Touch-friendly spell template positioning

## Requirements

- Foundry VTT v13+
- D&D 5e System 4.0+
- [socketlib](https://foundryvtt.com/packages/socketlib) module

## Installation

### From Foundry
1. Open Foundry VTT Setup
2. Go to Add-on Modules
3. Search for "Swipe VTT"
4. Click Install

### Manual Installation
Use this manifest URL:
```
https://github.com/crlngn/swipe-vtt/releases/latest/download/module.json
```

## Usage

The module automatically activates on mobile devices. On desktop, you can enable it manually in module settings.

### Touch Gestures
| Gesture | Action |
|---------|--------|
| Single tap | Select token |
| Double tap | Open character sheet |
| Long press | Show token HUD |
| Two-finger pan | Move canvas |
| Pinch | Zoom in/out |

## Premium Activation

1. Subscribe on [Patreon](https://www.patreon.com/carolingian)
2. In Foundry, open Swipe VTT settings
3. Click "Connect Patreon"
4. Authorize the connection
5. Premium features unlock automatically

## Support

- [Report Issues](https://github.com/crlngn/swipe-vtt/issues)
- [Patreon Community](https://www.patreon.com/carolingian)

## License

[CC-BY-NC-4.0](https://creativecommons.org/licenses/by-nc/4.0/) - See [LICENSE](LICENSE) for details.
