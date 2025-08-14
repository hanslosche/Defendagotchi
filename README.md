# 🐼 Defendagotchi
*A tiny cyber‑pet that levels up by protecting Wi‑Fi.*

![ESP32](https://img.shields.io/badge/platform-ESP32-black) ![Display](https://img.shields.io/badge/ILI9341-320×240-blue) ![Touch](https://img.shields.io/badge/XPT2046-touch-9cf)

> **Use ethically.** Detection only. Don’t disrupt networks. Only test gear you own or have permission to assess.

---

## What is it?
An ESP32 tamagotchi with a 240×320 ILI9341 touchscreen. Care for the pet (Feed, Pet, Play) to gain XP and unlock **real Wi‑Fi defense abilities**. At level 10, enable **Work Mode** to pause pet care and run all scanners.

**Highlights**
- Touch UI + optional hardware buttons
- Background deauth/portal/rogue monitoring
- Five built‑in scans (2.4 GHz)
- 13 color themes (Hacker, Vaporwave, Gameboy, etc.)

---

## Hardware
- ESP32 (VSPI for TFT; shared SPI for touch)
- ILI9341 320×240 (SPI) + XPT2046 touch
- Optional buttons to GND (active‑LOW)

**Pins (defaults)**
```
VSPI : SCK=18, MISO=19, MOSI=23
TFT  : CS=5, DC=2, RST=4   (RST=-1 ⇒ tie to EN)
TOUCH: CS=15, IRQ=27
BTN  : Feed=32, Pet=33, Play=25, Abilities=26, Work=21, Settings=13
```

---

## Install
1. Install **ESP32** board support in Arduino IDE.
2. Libraries: `Adafruit_GFX`, `Adafruit_ILI9341`, `XPT2046_Touchscreen`, `WiFi`, `HTTPClient`.
3. Open `Defendagotchi_ESP32_ILI9341_FIXED.ino` and flash.

> Portrait mode is used: `tft.setRotation(0)`, `ts.setRotation(0)`.

---

## Use
- **Main**: tap **Feed / Pet / Play / Abilities / Settings**.  
- **Abilities**: tap a row to run. **Back** at bottom.  
- **Settings → Themes**: tap = next, **hold 2s** = select, **double‑tap** = back.  
- **Work Mode** (Level ≥ 10): toggles from main screen.  
- **Serial dev keys**: `f,p,l` (care) · `1..5` (abilities) · `a/b/s/w/r` (screens/reset).

**Quick config**
```cpp
// Focus on your SSID (optional)
#define HOME_SSID "YourWiFiName"

// Touch alignment
#define TOUCH_SWAP_XY 1
#define TOUCH_FLIP_X  0
#define TOUCH_FLIP_Y  0
```

---

## Abilities
| Lvl | Ability | Summary |
|---:|---|---|
| 2 | **Deauth detector** | Counts deauth/disassoc frames while channel‑hopping. |
| 4 | **Rogue AP finder** | Flags SSID clones (same name, different BSSID). |
| 6 | **Portal check** | HTTP 204 test; detects captive portals/redirects. |
| 8 | **Channel overlap** | Reports most crowded 2.4 GHz channels. |
| 10 | **Weak encryption** | Counts Open/WEP APs in view. |

---

## Troubleshooting
- **Touch off / wrong button** → adjust `TOUCH_SWAP_XY`/`TOUCH_FLIP_*`, then fine‑tune `TS_MIN* / TS_MAX*`.  
- **Blank screen** → verify 3V3/GND and `TFT_CS/DC/RST`.  
- **“Cross‑wired” buttons** → check pins & `INPUT_PULLUP` wiring to GND; set `DEBUG_BTNS 1`.

---

## License
Choose a license (MIT recommended). PRs welcome.

---

**Built with** Adafruit GFX/ILI9341, XPT2046, and the ESP32 stack.
