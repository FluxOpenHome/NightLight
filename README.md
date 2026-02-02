# Flux Night Light

An open-source, ESPHome-powered night light built on the ESP32-C3 with a 16-LED WS2812 addressable LED array arranged in a 4x4 grid.

## Hardware

- **MCU:** ESP32-C3 (esp32-c3-devkitm-1)
- **LEDs:** 16x WS2812 individually addressable LEDs (GRB color order)
- **Data Pin:** GPIO10
- **LED Layout:** 4x4 grid in a snake wiring pattern

## Features

- **Home Assistant Integration** — Full control via the ESPHome API, including color picker, brightness slider, and effect selection
- **13 Built-in Effects:**
  - Pulse
  - Random
  - Strobe
  - Flicker
  - Addressable Rainbow
  - Addressable Color Wipe
  - Addressable Scan
  - Addressable Twinkle
  - Addressable Random Twinkle
  - Addressable Fireworks
  - Addressable Flicker
  - Fire (realistic flame simulation)
  - Flux Logo (animated logo display on the 4x4 grid)
- **State Persistence** — Color, brightness, and active effect are saved to flash and automatically restored after a power loss
- **OTA Updates** — Firmware updates delivered over HTTP from GitHub releases, with automatic update detection in Home Assistant
- **WiFi Provisioning** — Connect via Bluetooth LE (Improv) or serial for initial WiFi setup; fallback captive portal AP if WiFi is unavailable
- **Web Server** — Built-in web interface on port 80 for direct device control
- **Dashboard Import** — Supports ESPHome dashboard adoption for easy onboarding

## WiFi Setup

On first boot, the device creates a fallback hotspot:
- **SSID:** `flux-night-light-XXXXXX`
- **Password:** `12345678`

Connect to this AP and use the captive portal to enter your WiFi credentials. Alternatively, use the Improv BLE or serial provisioning from the ESPHome dashboard.

## OTA Firmware Updates

The night light checks for firmware updates from the GitHub releases manifest. When a new version is available, it appears as an update entity in Home Assistant. Updates can be triggered directly from the HA UI.

## Sensors & Diagnostics

The device exposes the following to Home Assistant:
- **Uptime** — How long the device has been running
- **WiFi Signal** — Current signal strength in dBm
- **IP Address** — Device IP on your network
- **Connected SSID** — WiFi network name
- **ESPHome Version** — Running firmware version
- **Firmware Update** — Update entity showing available versions

## LED Grid Layout

The 16 LEDs are wired in a snake pattern forming a 4x4 grid:

```
Row 4: LED 16  15  14  13   (right to left)
Row 3: LED  9  10  11  12   (left to right)
Row 2: LED  8   7   6   5   (right to left)
Row 1: LED  1   2   3   4   (left to right)
```

This layout enables grid-based effects like the Flux Logo, which maps specific LEDs to draw the logo shape.

## Alternative Firmware: WLED

If you prefer WLED over ESPHome, you can flash WLED onto this device. The only change needed is to set the LED data pin to **GPIO10** in the WLED LED settings:

1. Flash WLED for ESP32-C3 onto the device (via USB or web installer at [install.wled.me](https://install.wled.me))
2. Connect to the WLED AP and open the web UI
3. Go to **Config > LED Preferences**
4. Set the **GPIO** for the LED output to **10**
5. Set **LED count** to **16**
6. Set **Color order** to **GRB**
7. Save and reboot

That's it — WLED will work with the same hardware with no other modifications needed.

## Made for ESPHome

This project is designed to meet the [Made for ESPHome](https://esphome.io/guides/made_for_esphome/) program requirements:
- Open-source configuration, fully modifiable by end users
- All components have explicit IDs for extensibility
- No secrets or passwords in the base configuration
- Supports dashboard adoption via `dashboard_import`
- WiFi provisioning via Improv BLE and serial
- OTA update support

## License

See [LICENSE](LICENSE) for details.
