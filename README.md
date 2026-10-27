# Marlin 2.1.x — FLSun Q5 (Delta)

Firmware for the **FLSun Q5** Delta printer, based on the [Foxies-CSTL fork](https://github.com/Foxies-CSTL/Marlin_2.1.x) of Marlin, with `FLSUN_BUGFIX-MULTI` **merged against the latest upstream Marlin `bugfix-2.1.x`** (commit `5a946ab5f3`, 2026-10-26).

All FLSun Q-series tuning from the Foxies fork is preserved (multi-probe mesh, sensorless homing thresholds, delta calibration menus, preheat before probing, etc.).

## Printer / Board configuration (pre-set)

| Item | Value |
|---|---|
| Printer | FLSun **Q5** (`#define Q5` in `Marlin/FLSUNQ_Config.h`) |
| Motherboard | `BOARD_MKS_ROBIN_NANO` (Q5 old MoBo) |
| Stepper drivers | `STOCK` — 3× TMC2208 + 1× A4988 (stock Q5) |
| Leveling | Bed mesh, delta |
| `DELTA_HOME_TO_SAFE_ZONE` | **disabled** — after G28 the head stays raised at the safe position |
| Build environment | `mks_robin_nano_v1v2` (default in `platformio.ini`) |

> **Q5 2021 (new MoBo MKS Robin Nano V1.3 F4):** in `Marlin/FLSUNQ_Config.h` uncomment
> `#define MOTHERBOARD BOARD_MKS_ROBIN_NANO_V1_3_F4` and build with environment `mks_robin_nano_v1_3_f4`.

## Building

[PlatformIO](https://platformio.org) ≥ 6 is required (PlatformIO IDE / VS Code extension, or `pip install platformio`).

```bash
pio run -e mks_robin_nano_v1v2
```

The firmware is produced as `.pio/build/mks_robin_nano_v1v2/Robin_nano35.bin`.

Flash over USB (ST-Link / CH340 depending on your board revision), or via the board's USB bootloader per the FLSun update procedure.

## Branches

| Branch | Description |
|---|---|
| `FLSUN_BUGFIX-MULTI` | Foxies fork + upstream `bugfix-2.1.x` merge (2026-10-26) + Q5 config — **recommended** |
| `backup/q5-stable-config` | Pre-update snapshot of the old `FLSUN-STABLE` branch with the Q5 config |

## Updating from the Foxies fork

This repository is a merge on top of `Foxies-CSTL/Marlin_2.1.x`. To track future Foxies updates, use
[Foxies' repository](https://github.com/Foxies-CSTL/Marlin_2.1.x) branch `FLSUN_BUGFIX-MULTI` and re-apply the Q5 tweaks
(see [wiki](https://github.com/Foxies-CSTL/Marlin_2.1.x/wiki) for details):

- `Marlin/FLSUNQ_Config.h`: enable `#define Q5` (disable `QQSP`), disable `#define DELTA_HOME_TO_SAFE_ZONE`
- `platformio.ini`: `default_envs = mks_robin_nano_v1v2`

## Credits

- [Foxies-CSTL](https://github.com/Foxies-CSTL/Marlin_2.1.x) — FLSun Q-series optimized fork
- [MarlinFirmware/Marlin](https://github.com/MarlinFirmware/Marlin) — upstream
