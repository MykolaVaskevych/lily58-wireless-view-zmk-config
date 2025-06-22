# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a ZMK (Zephyr Mechanical Keyboard) firmware configuration for a Lily58 wireless split keyboard with Nice!View OLED displays. The repository uses GitHub Actions for automated firmware builds.

## Build Commands

### Automated Build (Recommended)
Push changes to GitHub and download firmware artifacts from the Actions tab.

### Local Build (Requires West and Zephyr SDK)
```bash
# Build left side
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD="lily58_left nice_view_adapter nice_view" -DZMK_CONFIG="${PWD}/config"

# Build right side
west build -s zmk/app -b nice_nano_v2 -- -DSHIELD="lily58_right nice_view_adapter nice_view" -DZMK_CONFIG="${PWD}/config"
```

## Architecture

### Key Files
- `config/lily58.keymap` - Main keymap definition with 6 layers and combos
- `config/lily58.conf` - ZMK configuration (Bluetooth power, debouncing, ZMK Studio)
- `build.yaml` - GitHub Actions build matrix configuration

### Keymap Structure
The keymap (config/lily58.keymap:20-215) defines:
- 6 layers: base, macos, farrows, symbols, gaming, bluetooth
- Home row mods on base and macOS layers
- Layer-switching combos using specific key combinations
- Balanced tap-hold behavior for modifier keys

### Hardware Configuration
- Board: nice_nano_v2
- Display: Nice!View with adapter
- ZMK Studio enabled for real-time keymap editing via USB

## Development Workflow

1. Modify `config/lily58.keymap` for layout changes
2. Update `config/lily58.conf` for feature toggles
3. Commit and push to trigger GitHub Actions build
4. Download .uf2 firmware files from Actions artifacts
5. Flash each keyboard half via USB bootloader mode