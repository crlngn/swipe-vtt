# Swipe VTT

A mobile-friendly interface for [Foundry VTT](https://foundryvtt.com/) with touch controls, optimized character sheets, and performance enhancements for phones and tablets. Use it as a second screen companion for easy access to character sheet, roll saves, skills, attacks, update of HP, etc. - but if your PC fails you can play from the phone!

If you are a Patreon supporter, as a GM all of your players will get access to premium features. The GM account needs to be logged in and connected to Patreon for them to be able to access premium features.

https://github.com/user-attachments/assets/7a10110e-a374-44f7-a0b4-386a25cb08b0


## Features

### AVAILABLE FOR FREE

- **Map Touch Controls** - Pan and pinch-zoom navigation on the canvas
- **Token Interaction** - Tap to select, tap again to target, double-tap to open sheets, drag to move, long-press for HUD
- **Quick controls** - quick access to most necessary controls: ruler, remove targets, template drawing, volume and logout
- **Touch/Mobile Detection** - Automatically enables on mobile devices
- **Portrait/Landscape Support** - Adapts UI to device orientation - on tablets, sheets load as a side drawer
- **Safari Compatibility** - Fixes for iOS Safari quirks (But JB2A videos don't have transparency on iOS, can't work around)
- **Performance adjustments** - Tweaks to improve frame rate and overheating on devices
- **Application window resize** - resizes or rescales handouts, journals and other application windows to fit in view
- **Character carousel** - see all characters you have ownership to in the swipable carousel
- **Basic sheet** - tab for basic rolls as well as hp management is free (DnD5e / Daggerheart)

### FOR PATREON SUPPORTERS (Amethyst tier)

Premium features require a [Patreon](https://www.patreon.com/carolingiandev) subscription on Amethyst tier

- **Full Mobile Character Sheets** - Drawer UI with all tabs - Inventory, Features, Spells, and a Combat section (currently for DnD5e / Daggerheart)
- **Combat Section** - Quick access to attacks, saves, and ability checks
- **Inventory and Spellbook** - Touch-friendly lists with activation and preparation buttons
- **Canvas Freeze** - Enable on low-end devices to help conserve battery and improve performance - canvas remains frozen when unused
- **Image Optimizer** - Compress scene backgrounds and tokens for faster loading
- **Chat Drawer** - Slide-out chat panel optimized for mobile
- **Spell Template Placer** - Touch-friendly spell template positioning - combine with free module **Flash Token Bar** for auto-targeting

The module hs been tested and works well with **Midi-QoL**, **Flash Token Bar** and **Carolingian UI**

### Limitations

- JB2a videos don't work on iPad / iPhone - you can disable them in settings
- Sheet editing is for combat-related things - not character management
- Not extensively tested on old phones

## Requirements

- Foundry VTT v13+
- [socketlib](https://foundryvtt.com/packages/socketlib) module
- For sheets: D&D 5e System 4.0+ or Daggerheart

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

- The module automatically activates on mobile devices
- The GM must have connected in the last 7 days for players to use the premium features offline

### Touch Gestures
| Gesture | Action |
|---------|--------|
| Single tap | Select token <-> Target token |
| Double tap | Open character sheet |
| Drag | Move token |
| Long press | Show token HUD |
| Two-finger pan | Move canvas |
| Pinch | Zoom in/out |

## Premium Activation

1. Subscribe on [Patreon](https://www.patreon.com/carolingiandev)
2. In Foundry, open game settings >> Swipe VTT 
3. Connect to Patreon
  - As GM: if you are on a desktop browser, you can connect to Patreon via Connect to Patreon button
    A popup should appear for you to connect to Patreon and validate your membership
  - As GM: if you login on mobile device or Foundry Desktop App, the popup above won't work. 
    Instead, use the "Authenticate with Link Code" option to get a code and paste it on the input box
4. Authorize the connection
5. Premium features unlock automatically for GM and players

## Support
- [Discord](https://discord.gg/kjmJzgUJ)
- [Patreon Community](https://www.patreon.com/carolingiandev)
- [Report Issues](https://github.com/crlngn/swipe-vtt/issues)

## License

[CC-BY-NC-4.0](https://creativecommons.org/licenses/by-nc/4.0/) - See [LICENSE](LICENSE) for details.
