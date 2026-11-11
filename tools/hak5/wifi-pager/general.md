# General

## About

Two decades of WiFi exploits & payload mastery have come together. Pocket-sized. DuckyScript™ powered.

With the Pager, you get real-time WiFi alerts with ringtones and vibrations. Then, command the airspace with a full suite of attacks, intelligent reconnaissance and payload–powered mayhem.

* Tri-Band WiFi + Bluetooth & BTLE
  * 2.4 GHz, 5 GHz, 6 GHz - dual radio array
* 2000 mAh Battery with USB-C charging and integrated Ethernet adapter
* Vivid color display; high resolution, crisp from any angle, indoors and out
* 4 GB EMMC, 256 MB RAM, USB 2.0, 4x RGB LED, Buzzer, Vibration, RTC

### What makes it different

The Pager is essentially a **pocket-sized, battery-powered WiFi Pineapple** with an on-device color screen and D-pad, so you can run recon, PineAP, and payloads untethered - no laptop required. It is **tri-band (2.4 / 5 / 6 GHz)** for monitoring, where the Mark VII is primarily 2.4 GHz. Everything is driven by **DuckyScript payloads**, and the device can alert you physically (ringtone + vibration) the moment something interesting happens in the air.

> ⚠️ **Receive/monitor focused.** As with all Hak5 WiFi gear, only operate it against networks and clients you are authorized to test. Keep your PineAP filters tight (see \[\[PineAP]]).

### Hardware at a glance

| Component  | Detail                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| Radios     | Tri-band 2.4 / 5 / 6 GHz monitor radio (`wlan1mon`); client mode is **2.4 GHz only** (`wlan0cli`); management AP on `wlan0mgmt`. Bluetooth + BTLE.  |
| CPU        | MIPS (little-endian, `mipsel`) - matters when building/installing payload binaries.                                                                 |
| Storage    | 4 GB eMMC holds `/root`, payloads, loot, themes. The writable root overlay has **< 32 MB free** after firmware - install extra packages to the MMC. |
| RAM        | 256 MB                                                                                                                                              |
| Battery    | \~4 hours per charge; USB-C charging.                                                                                                               |
| USB-C port | Data + charging. Presents to a host as a **Realtek RTL8153 USB Ethernet** device (the Pager hands your computer an IP via DHCP).                    |
| USB-A port | For a **GPS receiver** or a USB Ethernet adapter.                                                                                                   |
| Display    | Vivid color display; theme backgrounds are **480×222 px** (see \[\[Themes]]).                                                                       |
| Extras     | 4× RGB LED, buzzer, vibration motor, RTC.                                                                                                           |

### Buttons & LEDs

* **D-pad** - Up / Down / Left / Right for navigation.
* **A button (green)** - activate / confirm / go forward.
* **B button (left-most, red)** - cancel / back.
* **Power button** - recessed, top-left. Hold **3–4 s to power on**; **double-tap** for the power menu (clean shutdown, lock, UX stats); hold **5 s to force power-off**.
* **Charge LED** - **solid red** while charging, **solid green** when fully charged. Red + green blink together during factory reset and firmware recovery.

> The device **may get warm** in use - that's expected.

### Links

* [Shop Page](https://shop.hak5.org/products/wifi-pineapple-pager)
* [Setup](https://shop.hak5.org/pages/pager-setup)
* [Docs](https://docs.hak5.org/wifi-pineapple-pager/)
* [Firmware downloads](https://downloads.hak5.org/pineapple/pineapplepager)
* [Payloads repo](https://github.com/hak5/wifipineapplepager-payloads)
* [Themes repo](https://github.com/hak5/wifipineapplepager-themes)

## Usage

### First-time setup

1. **Charge fully** - the charge light goes from **red to green**.
2. **Download the latest firmware** from [the firmware page](https://downloads.hak5.org/api/devices/wifipineapplepager/firmwares/latest) (verify the checksum; avoid third-party firmware).
3. **Power on** (hold the power button 3–4 s). First boot takes \~3–4 minutes.
4. **Plug your computer into the Pager's USB-C port.** Your computer detects it as a **USB Ethernet adapter** and automatically gets an IP on the `172.16.52.0/24` network.
5. Open a browser to [**http://172.16.52.1:1471**](http://172.16.52.1:1471) and follow the on-screen instructions.
6. Upload the firmware. **Flashing + first boot takes \~10–15 minutes.**
7. Complete the setup screens: **PIN code → root password → timezone → accept the** [**Hak5 license**](https://hak5.org/license).

> **Addressing cheat-sheet** - the Pager uses the `172.16.52.0/24` network on both the USB-C and Management interfaces:
>
> * **Web / Virtual Pager UI:** `http://172.16.52.1:1471` (always include the `:1471`, or the browser may redirect to HTTPS or a search).
> * **SSH:** `ssh root@172.16.52.1` (port 22, root password set during setup).
> * **Firmware recovery:** `http://172.16.52.1` (plain HTTP, no port).

### The on-device dashboard

The main dashboard exposes these panels:

* **Alerts** - surfaces Alert payloads raised by events from nearby devices (see \[\[Payloads]]).
* **Payloads** - launch User payloads.
* **Recon** - passive 2.4/5 GHz (6 GHz optional) monitoring. The list auto-updates the 5 most recent/strongest devices; **Up/Down pauses** it and the refresh icon resumes. **A** opens device details; from there you can run **Recon payloads**. A graph view is available (Left/Right change the data shown; **A** opens recon settings - audio modes, bands). The status bar shows Wigle logging, GPS status, recon logging, PCAP logging, brightness, enabled bands, battery, and time.
* **PineAP** - rogue AP suite: Open AP, EvilWPA, SSID pool, filters, client list (see \[\[PineAP]]).
* **Settings** - **Network** (Client Mode Setup, Management AP Setup, 6 GHz), **GPS**, **Updates**.

### Updating

* **On device:** `Settings → Updates → Check for Updates` (needs internet and an accurate clock).
* **Over SSH:** `scp` the firmware to `/tmp`, then `INSTALL_FIRMWARE /tmp/<file>`. Upgrades keep `/root` and your configuration but drop `opkg` packages installed in the root overlay.

### Factory reset / recovery

* **Factory reset:** hold **B** at power-on, then **A** to start. Erases the eMMC including `/root`.
* **Firmware recovery:** hold **A** at power-on, connect USB-C, then browse to `http://172.16.52.1`.

### Related notes

* \[\[Payloads]] - writing and installing DuckyScript payloads
* \[\[PineAP]] - rogue AP configuration and filtering
* \[\[Themes]] - custom UI themes
* \[\[Wardriving]] - GPS + Wigle logging
