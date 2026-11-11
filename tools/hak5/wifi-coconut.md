# 🥥 WiFi Coconut

## About

The [Hak5 WiFi Coconut](https://shop.hak5.org/products/wifi-coconut) is an open-source, full-spectrum 2.4 GHz WiFi sniffer. Where a typical WiFi adapter in monitor mode can only listen to a single channel at a time (forcing you to "channel hop" and miss traffic on every channel you aren't currently on), the Coconut packs **14 dedicated 802.11 radios**, one per 2.4 GHz channel, so it monitors the **entire 2.4 GHz airspace simultaneously**.

It captures standard **PCAP** files and integrates cleanly with the tools security researchers already use: **Wireshark**, **tshark**, **tcpdump**, and **Kismet**.

#### Why full-spectrum matters

* **No missed frames.** Single-radio adapters hop channels, so a management/data frame on channel 6 is lost while the radio is parked on channel 1. The Coconut listens to all 14 at once.
* **Complete captures.** Great for RF surveys, deauth/association analysis, rogue-AP hunting, and research where losing frames corrupts the picture.
* **Receive-only by design.** The Coconut is a _passive_ sniffer. See the warning below.

> ⚠️ **Do NOT transmit with the WiFi Coconut radios.** Transmitting may damage the device and voids the Hak5 limited warranty. Use monitor-mode / capture tools only - never injection tools like Aircrack-ng's attack modes against the Coconut radios.

### Channels & Radios

* The 2.4 GHz band has **14 channels** worldwide; the Coconut has one radio per channel.
* Regulatory domains differ: the **US uses channels 1–11**, and **Japan may unlock 12–14**. Which radios see traffic depends on what's legal/in-use in your region.
* The radios are **Ralink/MediaTek RT5370**-based (USB ID `148f:5370`), using the `rt2800usb` driver family.

### Hardware Notes

* **Two USB-C ports:**
  * **USB Data Port** - carries both data and power. In most cases this is the only port you need.
  * **Aux Power Port** - supplies extra power when the host can't power all 14 radios over a single cable.
* ⚠️ **Do not use the Aux Power Port with a USB-C PD (Power Delivery) device** - the Coconut will fail to enumerate as a USB device. If you need more power, use a USB-C-to-USB-A adapter into a powered hub instead.
* **Use a high-quality USB-C cable.** 14 radios draw more current than cheap cables reliably deliver; a poor cable shows up as missing radios or unstable captures.
* **Host requirements:** Older machines (early-2010s era) may fail with errors like _"Not enough USB3 resources"_ on Windows - use a newer host.
* **Raspberry Pi:** A **Pi 4 with external power** works. The **Pi 3's** USB subsystem is not sufficient.

## Links

* [Store Page](https://shop.hak5.org/products/wifi-coconut)
* [Documentation](https://docs.hak5.org/wifi-coconut/wifi-coconut-by-hak5/)
* [GitHub - hak5/hak5-wifi-coconut](https://github.com/hak5/hak5-wifi-coconut)
* [Kismet integration docs](https://docs.hak5.org/wifi-coconut/capture-files/kismet/)

## Setup / Installing

### Linux

#### Install build dependencies

**Debian / Ubuntu / Kali / Parrot**

```bash
sudo apt install build-essential cmake libusb-1.0-0-dev libpcap-dev git
```

**RHEL / Fedora**

```bash
sudo dnf install cmake automake gcc gcc-c++ kernel-devel git
```

**Arch**

```bash
sudo pacman -S base-devel cmake libpcap libusb git
```

#### Build and install

```bash
git clone https://github.com/hak5/hak5-wifi-coconut && cd hak5-wifi-coconut
mkdir build && cd build
cmake ../
make
sudo make install
```

By default this installs the `wifi_coconut` binary to `/usr/local/bin` and the `rt2800usb` firmware to `/usr/local/share/`.

### macOS

```bash
brew tap hak5/wifi-coconut
brew install wifi-coconut
```

Requires the Xcode command-line tools. Building from source instead needs `cmake` and `libusb` from Homebrew. On macOS the tool is run **without** `sudo` (just `wifi_coconut`).

### Windows

1. Install the **Zadig** WinUSB driver (from [zadig.akeo.ie](https://zadig.akeo.ie)).
2. Select a radio listed as **"802.11n WLAN"** with USB ID **`148F 5370`**, choose **Replace Driver**, and install **WinUSB**.
3. Download the **win64** tools from [downloads.hak5.org/coconut](https://downloads.hak5.org/coconut), unzip, and run `wifi_coconut.exe`.

> ⚠️ Installing the Zadig/WinUSB driver for the rt2800 chipset will **disable other WiFi cards that use the same chipset**. If your only WiFi is a USB adapter, confirm your built-in card doesn't use rt2800 first. The Windows binary is unsigned and may trigger a SmartScreen/AV warning.
>
> ℹ️ Kismet does **not** work on Windows - WSL/WSL2 can't pass the USB device through.

## Running

Launched with no options, the tool opens an **interactive mode** showing a per-channel UI. Root/admin is required because it performs raw USB access.

```bash
sudo wifi_coconut
```

(On macOS, run `wifi_coconut` without `sudo`.)

### Command-line options

> The reference below mirrors the published usage text. The official docs have a formatting glitch around the wait-related flags, so **always confirm against `wifi_coconut --help` on your installed build.**

**Universal options**

| Option               | Description                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------- |
| `--disable-leds`     | Go fully dark - don't enable any LEDs.                                                                  |
| `--invert-leds`      | Normally all LEDs are on and blink during traffic; inverted, LEDs light **only** when there is traffic. |
| `--disable-blinking` | Keep LEDs on but stop them blinking on traffic.                                                         |

**Non-interactive modes**

| Option                          | Description                                                                                   |
| ------------------------------- | --------------------------------------------------------------------------------------------- |
| `--no-display`                  | Don't draw the channel UI while logging (needed when piping).                                 |
| `--wait` / `--wait-for-coconut` | Wait for a Coconut to be connected and identified before starting.                            |
| `--pcap=[fname]`                | Log packets to a PCAP file. Use `-` to echo the PCAP to **stdout** for piping to other tools. |
| `--list-coconuts`               | List connected WiFi Coconut devices and exit.                                                 |
| `--coconut-device=X`            | Select which Coconut to use when multiple are connected.                                      |
| `--enable-partial`              | Enable a Coconut even if not all 14 radios were identified.                                   |
| `--plain-dot11`                 | Log plain 802.11 frames instead of radiotap-wrapped frames (drops signal/channel metadata).   |
| `--quiet`                       | Disable most output.                                                                          |

## PCAP Output

* `--pcap=<file>` writes a standard PCAP file; `--pcap=-` streams it to stdout.
* By default each packet is wrapped in a **radiotap** header (added by the userspace radio drivers), carrying **signal strength and channel** metadata outside the 802.11 frame.
* `--plain-dot11` strips the radiotap header, logging plain 802.11 frames with no signal/channel fields.

## Running with other tools

### TCPDump

```bash
sudo wifi_coconut --no-display --pcap=- | tcpdump -r -
```

### TShark

```bash
sudo wifi_coconut --no-display --pcap=- | tshark -r -
```

### Wireshark

Open a saved capture directly:

```bash
sudo wifi_coconut --no-display --pcap=capture.pcap
# then open capture.pcap in Wireshark
```

Wireshark is available on Linux, macOS, and Windows.

### Kismet

Kismet has integrated the WiFi Coconut capture tool since the **2022-08-11-nightly** build. More info: [Coconut + Kismet docs](https://docs.hak5.org/wifi-coconut/capture-files/kismet/).

Install (Kismet package repositories must be added first - see the Kismet install docs):

```bash
sudo apt install kismet
sudo apt install kismet-capture-hak5-wifi-coconut
```

Prebuilt packages exist for Kali, Ubuntu Focal, and Ubuntu Jammy on `amd64`, `arm64`, and `armhf`. Building Kismet from source instead requires the `--enable-wifi-coconut` configure flag.

*   **List connected Coconuts**

    ```bash
    kismet_cap_hak5_wifi_coconut --list
    ```

    Sample output: `coconut-2 (Hak5 Wi-Fi Coconut)`
*   **Start Kismet with the Coconut**

    ```bash
    kismet -c coconut:name=WifiCoconut
    ```

    You can also target a specific device (e.g. `coconut-2`), or just `coconut` if only one is connected. In the Kismet UI, select the Coconut under **Datasources** - the individual raw radio interfaces then disappear.

> The Kismet capture helper must run as **root**. The package install offers to set the Kismet tools suid-root; otherwise set the binary suid-root or run Kismet as root.
>
> **Linux-only:** you can alternatively add the 14 raw radios as individual Kismet sources and let Kismet distribute channels across them - the docs flag this as "use at your own risk." Kismet works on macOS only via a source build, and not at all on Windows.
>
> ⚠️ Kismet uses monitor mode only, which is safe. Never point transmit-capable tools (e.g. Aircrack-ng attacks) at the Coconut radios.

## Troubleshooting

*   **Confirm all 14 radios enumerate:**

    ```bash
    lsusb | grep '148f:5370'
    ```

    You should see **14** entries, each a Ralink RT5370 Wireless Adapter. Fewer entries usually means a weak cable or insufficient power.
*   **Check kernel messages** if radios are missing:

    ```bash
    sudo dmesg
    ```
* **Power/cable issues:** use a high-quality USB-C cable, a newer host, and add external aux power if needed (but **not** via a USB-C PD device - see Hardware Notes).
* **macOS:** older releases (Catalina, Big Sur) had a kernel USB bug - quit other apps that touch USB (including browsers like Chrome). Fixed in Monterey and newer.
* **Windows:** if Device Manager shows Microsoft drivers instead of libwdi/WinUSB, the Zadig install didn't take - redo the Zadig steps.
* **Permissions:** `wifi_coconut` (Linux) and Kismet capture both require **root**.
* You _can_ fall back to the OS's default `rt2800usb` drivers instead of the Coconut tools, but this is **not recommended**.
