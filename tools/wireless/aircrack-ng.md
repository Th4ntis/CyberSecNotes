# Aircrack-ng

## About

Aircrack is a popular and powerful WiFi penetration testing tool used to assess WiFi network security. This focuses on monitoring, attacking, testing, and cracking.&#x20;

[Aircrack-ng homepage](https://www.aircrack-ng.org/)

[Aircrack-ng github](https://github.com/aircrack-ng/aircrack-ng)

## Install

On debian based linux distros you can run `sudo apt install aircrack-ng`. This will install version 1.6. If you want to install from source I typically:

sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev ethtool shtool rfkill zlib1g-dev libpcap-dev libsqlite3-dev libpcre3-dev libhwloc-dev libcmocka-dev hostapd wpasupplicant tcpdump screen iw usbutils

`cd /opt/ && sudo git clone` [`https://github.com/aircrack-ng/aircrack-ng.git`](https://github.com/aircrack-ng/aircrack-ng.git) `&& cd aircrack-ng`

`sudo autoreconf -i`

`sudo ./configure --with-experimental`

`sudo make`

`sudo make install`

`sudo ldconfig`

## Usage

* `airmon-ng` - Enables monitor mode for WiFi chipsets that support it.
  * Eg. `airmon-ng start wlan1`
* `airodump-ng` - Scans for WiFi from selected WiFi interface
  * Eg. `airodump-ng wlan1mon` - Scans for all networks
  * Eg. `airodump-ng -c 1 -o scan.cap --bssid 11:22:33:44:55:66 wlan1mon` - Focuses on targeted network, replacing 1 with the channel of the targets WiFi channel and 11:22:33:44:55:66 with the targets MAC Address.
* `aireplay-ng` - Used to inject frames in various forms.
  * Eg. `aireplay-ng -0 5 -a 11:22:33:44:55:66 wlan1mon`
* `aircrack-ng` - Cracks captured handshakes that are in .cap file form.&#x20;
  * Eg. `aircrack-ng -w /opt/SecLists/Passwords/rockyou.txt scan.cap`
