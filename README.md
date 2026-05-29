# xiaomi-mb5a-fix

A custom component for Home Assistant that adds support for the **Xiaomi Air Purifier 4 Rev A** (`zhimi.airp.mb5a`).

This is a drop-in replacement for the built-in `xiaomi_miio` integration with one targeted fix: the `mb5a` hardware revision is not yet in `python-miio`'s device mapping table (the library has not had a stable release since 2022), so without this fix HA falls back to the wrong property mapping and the device appears broken.

The fix aliases `zhimi.airp.mb5a` to `zhimi.airp.mb5` (Air Purifier 4) in HA's device creation path. The two models share identical MIoT properties, confirmed by querying a live `mb5a` device.

> **Note:** This uses the same domain (`xiaomi_miio`) as the built-in integration, so it completely replaces it. All your other Xiaomi devices should continue to work normally — the only change is the addition of `mb5a` support.

## Installation

1. Copy the `custom_components/xiaomi_miio` folder into your HA config directory:
   ```
   <ha-config>/custom_components/xiaomi_miio/
   ```
2. Restart Home Assistant.
3. Add the device via **Settings → Devices & Services → Add Integration → Xiaomi Home**, using your device's IP and token.

## Goal

The intent is to get this fix merged into HA core. This repo exists for testing purposes while the PR is in review.

Upstream tracking:
- [python-miio](https://github.com/rytilahti/python-miio) — the underlying library (needs `zhimi.airp.mb5a` added to its model mapping)
- [home-assistant-core](https://github.com/home-assistant/core) — where the permanent fix will land
