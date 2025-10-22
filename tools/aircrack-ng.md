# Aircrack-NG

## About

Aircrack is a popular and powerful WiFi penetration testing tool used to assess WiFi network security. This focuses on monitoring, attacking, testing, and cracking.

### Links

[Aircrack-ng homepage](https://www.aircrack-ng.org/)

[Aircrack-ng github](https://github.com/aircrack-ng/aircrack-ng)

## Install

On debian based linux distros you can run `sudo apt install aircrack-ng`. This will install version 1.6. If you want to install from source I typically:

```
sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev ethtool shtool rfkill zlib1g-dev libpcap-dev libsqlite3-dev libpcre3-dev libhwloc-dev libcmocka-dev hostapd wpasupplicant tcpdump screen iw usbutils
cd /opt/ && sudo git clone 
https://github.com/aircrack-ng/aircrack-ng.git
 && cd aircrack-ng
sudo autoreconf -i
sudo ./configure --with-experimental
sudo make
sudo make install
sudo ldconfig
```

## Usage

* `airmon-ng` - Enables monitor mode for WiFi chipsets that support it.
  * Eg. `airmon-ng start wlan1`
* `airodump-ng` - Scans for WiFi from selected WiFi interface
  * Eg. `airodump-ng wlan1mon` - Scans for all networks
  * Eg. `airodump-ng -c 1 -o scan.cap --bssid 11:22:33:44:55:66 wlan1mon` - Focuses on targeted network, replacing 1 with the channel of the targets WiFi channel and 11:22:33:44:55:66 with the targets MAC Address.
* `aireplay-ng` - Used to inject frames in various forms.
  * Eg. `aireplay-ng -0 5 -a 11:22:33:44:55:66 wlan1mon`
* `aircrack-ng` - Cracks captured handshakes that are in .cap file form.
  * Eg. `aircrack-ng -w /opt/SecLists/Passwords/rockyou.txt scan.cap`

## Hotkey shortcuts for Airodump

* `a` - Select active areas by cycling through these display options: AP+STA; AP+STA+ACK; AP only; STA only
* `l` - Invert sorting algorithm
* `M` - Mark the selected AP or cycle through different colors if the selected AP is already marked
* `R` - (De-)Activate realtime sorting - applies sorting algorithm everytime the display will be redrawn
* `S` - Change column to sort by, which currently includes: First seen; BSSID; PWR level; Beacons; Data packets; Packet rate; Channel; Max. data rate; Encryption; Strongest Ciphersuite; Strongest Authentication; ESSID
* `Space` - Pause display redrawing/ Resume redrawing
* `Tab` - Enable/Disable scrolling through AP list
* `O` - Toggle color on
* `P` - Toggle color off
* `Up Arrow` - Select the AP prior to the currently marked AP in the displayed list if available
* `Down Arrow` - Select the AP after the currently marked AP if available
