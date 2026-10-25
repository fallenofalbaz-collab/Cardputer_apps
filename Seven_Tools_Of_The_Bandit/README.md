# Seven Tools of the Bandit

A sysadmin multi-tool firmware for the **M5Stack Cardputer v1** (ESP32-S3).
29 network/sysadmin tools across 7 categories, a bilingual (Spanish/English)
UI, a physical lock screen, and a vector-drawn pirate-knife welcome screen —
no bitmap UI assets, everything is drawn live on the 240×135 display.

![Splash screen](docs/images/01_splash.png)
![Welcome screen](docs/images/02_welcome.png)

## Highlights

- **29 tools, 7 categories** — WiFi, Probe, Monitor, Local Net, USB HID,
  Files, Server. See the full list below.
- **Bilingual UI** — press **L** on the launcher or a submenu to switch
  the whole app between Spanish and English, including every tool
  screen, its detailed help block, and its status/toast messages.
- **Screen lock** — the physical **G0** button locks/unlocks the device,
  showing "Raimu" (an original pixel-art mascot by the project's author)
  with a gentle idle bob; the onboard WS2812 LED changes color with
  activity/state.
- **Clock + battery** in the header (NTP time, with a graceful "+HH:MM"
  uptime fallback when there's no network to sync against).
- **Easter egg** — while the screen is locked, pressing **ENTER** or any
  arrow key makes Brisa (the author's own dog character, from a separate
  Cardputer project) run across the bottom of the screen for a few loops,
  without unlocking the device.
- **QR connection code** — the file server screen can render a QR code
  with its own WiFi connection details.
- **`7tools.cfg`** on the SD card remembers known WiFi passwords so the
  device reconnects automatically.

![Launcher menu](docs/images/03_launcher.png)
![Submenu example](docs/images/04_submenu.png)

## The 7 categories / 29 tools

| Category | Tools |
|---|---|
| **WIFI** | WiFi Scan · Network Info · Saved Networks · Twin Alert (duplicate-SSID detector) · Network History |
| **PROBE** | Ping (TCP) · Port Scan · Traceroute (TTL-based) · HTTP Client · DNS lookup |
| **MONITOR** | Packet Monitor (live traffic graph) · WiFi Channels · Device Count · Live Signal · Free Channel finder |
| **LOCAL NET** | Subnet Calculator · Wake on LAN · Password Generator · Range Check · IP Converter |
| **USB HID** | USB Keyboard passthrough · USB Mouse passthrough · Keyboard Combos · Presenter (remote slide control) |
| **FILES** | SD Explorer (create/delete/copy/move/rename/preview) · SD Space usage |
| **SERVER** | Own Network (AP) file server · On My Network (STA) file server · Access Log |

![Packet Monitor](docs/images/05_packet_monitor.png)

## Screen lock + easter egg

![Lock screen](docs/images/06_lock_screen.png)
![Brisa easter egg](docs/images/07_lock_screen_brisa.png)

## What's deliberately *not* here

Earlier in development, deauthentication attacks, an Evil-Twin / captive
portal simulator, and a WiFi probe-sniffer (which tracks nearby device
owners) were requested and turned down: those are attack/interference and
non-consensual-tracking tools, not diagnostics, regardless of "educational"
or "own network" framing. The **Packet Monitor** tool only counts
management/data/control packet *types* on the current channel — it never
inspects packet contents or targets a specific device.

## Controls

```
; .     move selection
ENTER   open category / tool
`       back / exit
i       this screen's help
M       mute sound
L       switch language ES/EN (launcher/submenu)
G0      lock screen
```

## Hardware

- M5Stack Cardputer v1 (ESP32-S3 / StampS3)
- 240×135 display, WS2812 status LED (GPIO21)
- microSD over SPI (CS=12, SCK=40, MISO=39, MOSI=14)
- USB HID keyboard/mouse passthrough via TinyUSB

## Pre-built releases

The [`builds/`](builds) folder has ready-to-flash `.bin` files, in order:

| File | Notes |
|---|---|
| `7tools-of-the-bandit-v1.bin` | Early build |
| `7tools-of-the-bandit-v2.bin` | |
| `7tools-of-the-bandit-v3.bin` | |
| `7tools-of-the-bandit-v4.bin` | |
| `7tools-of-the-bandit-v5.bin` | |
| `7tools-of-the-bandit-v6.bin` | |
| `7tools-of-the-bandit-v7-final.bin` | **Latest — recommended** |

Flash the latest one (`v7-final`) with the M5Launcher, or any ESP32 flashing
tool pointed at the Cardputer's app partition.

## Build from source

This is a [PlatformIO](https://platformio.org/) project using the Arduino
framework and the M5Cardputer/M5Unified library. Full source lives in the
sibling repo [`7toolsoftheBandit`](https://github.com/fallenofalbaz-collab/7toolsoftheBandit/tree/main/cardputer).

```bash
pio run                 # build
pio run --target upload # flash
```

## Credits

Firmware design and all artwork (welcome-screen knife illustration, the
"Raimu" chibi mascot on the lock screen) are original work by the
project's author. The Brisa sprite used in the lock-screen easter egg is
cropped from the author's own "Talking Dog" project spritesheet.
