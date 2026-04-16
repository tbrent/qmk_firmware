# QMK Firmware - Personal Fork

## My Keyboard

BastardKB Charybdis 4x6 V2 with Splinky 3 (RP2040) controller. Trackball is disabled.

- **Keymap location**: `keyboards/bastardkb/charybdis/4x6/keymaps/mine/`
- **Physical keyboard target**: `bastardkb/charybdis/4x6/v2/splinky_3` (what QMK Configurator calls it)
- **Compile target**: `bastardkb/charybdis/4x6/elitec` with `CONVERT_TO=elite_pi` converter (the `v2/splinky_3` variant was removed from mainline QMK; the `elitec` target with `elite_pi` converter maps Elite-C pins to RP2040)

## Compile Command

```sh
export PATH="/opt/homebrew/opt/arm-none-eabi-binutils/bin:/opt/homebrew/opt/arm-none-eabi-gcc@8/bin:/Users/tbrent/.asdf/installs/python/3.10.4/bin:$PATH"
qmk compile -kb bastardkb/charybdis/4x6/elitec -km mine -e CONVERT_TO=elite_pi
```

Output: `bastardkb_charybdis_4x6_elitec_mine_elite_pi.uf2` (RP2040 uses .uf2, not .hex)

## Flash Instructions

1. Enter bootloader: double-tap reset button, or press `QK_BOOT` key (layer 3, top-left)
2. Board appears as USB drive `RPI-RP2`
3. Drag .uf2 onto the drive

## Layout Notes

- Colemak base layer with 4 layers total (base, nav, symbols/numpad, macros)
- Trackball disabled via `POINTING_DEVICE_ENABLE = no` in keymap's `rules.mk`
- Tapping term set to 130ms with `PERMISSIVE_HOLD` in keymap's `config.h`
- Thumb cluster: 5 upper keys (3 left + 2 right) then 3 lower keys (2 left + 1 right) = 8 total. When editing the keymap JSON, the thumb section is the last 8 entries per layer.

## Required Submodules

```sh
git submodule update --init --recursive lib/chibios lib/chibios-contrib lib/pico-sdk lib/printf lib/lufa
```

## Dependencies (macOS)

```sh
brew install osx-cross/arm/arm-none-eabi-gcc@8 osx-cross/arm/arm-none-eabi-binutils
pip3 install qmk
```
