# HCXDumptool

## About

HCSDumptool is a "Small tool to capture packets from wlan devices and to discover potential weak points within own WiFi networks (e.g.: PreSharedKey or PlainMasterKey is transmitted unencrypted by a CLIENT)."

[HCXDumptool Github](https://github.com/ZerBea/hcxdumptool)

## Install

`sudo apt install -y libcurl4-openssl-dev libssl-dev pkg-config`

`cd /opt/`

`sudo git clone https://github.com/ZerBea/hcxdumptool.git && cd hcxdumptool`

`sudo make`

`sudo make install`

## Usage

First you must designate your target in a file. You can name the file whatever you want, but it must contain the the MAC address of the target network(s) without colons. In my example the file will be called target.

`hcxdumptool -o (SSID/Name) -i wlan0mon --filterlist_ap=target --filtermode=2 --enable_status=3`

* \[PMKIDROGUE]: The PMKID is requested by hcxdumptool and not by a CLIENT
* \[M1M2ROGUE]: EAPOL M2 is requested from a CLIENT by hcxdumptool and not from an AP.
* \[PMKID: KDV:2]: You captured a PMKID requested from a CLIENT.

If an AP recieves our association request packet and supports sending PMKID we will see a message "FOUND PMKID" after a moment.

\[TIME - 011] 89acf0e761f4 -> 4604ba734d4e (SSID) \[ASSOCIATIONREQUEST, SEQUENCE 4]

\[TIME - 011] 4604ba734d4e -> 89acf0e761f4 \[ASSOCIATIONRESPONSE, SEQUENCE 1206]

\[TIME - 011] 4604ba734d4e -> 89acf0e761f4 \[FOUND PMKID]
