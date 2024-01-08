# Bettercap

## About

Bettercap is "The Swiss Army knife for [WiFi](https://www.bettercap.org/modules/wifi/), [Bluetooth Low Energy](https://www.bettercap.org/modules/ble/), wireless [HID hijacking](https://www.bettercap.org/modules/hid/) and [IPv4 and IPv6](https://www.bettercap.org/modules/ethernet) networks reconnaissance and MITM attacks."

[Bettercap Homepage](https://www.bettercap.org/)

[Bettercap Github](https://github.com/bettercap/bettercap)

## Install

There's multiple ways to install bettercap, they have documentation [here](https://www.bettercap.org/installation/). I typically install from source. Currently having [Go installed](https://go.dev/doc/install).

`go install github.com/bettercap/bettercap@latest`

`sudo ~/.go/bin/bettercap -eval "caplets.update; ui.update; q"`

## Usage

Running `bettercap` in the terminal will allow you to run bettercap via the commandline and will be met with the bettercap prompt. Edit the default credentials for the web interface at `/usr/local/share/bettercap/caplets/http-ui.cap` and/or `/usr/local/share/bettercap/caplets/http-ui.cap`. You can also run via the web interface via `sudo bettercap -caplet http-ui` OR `sudo bettercap -caplet https-ui`. Then you can go to [http://127.0.0.1/](http://127.0.0.1/) OR [https://127.0.0.1/](http://127.0.0.1/).

![](<../../.gitbook/assets/image (210).png>)

### Command Line

Change interface mac and put interface into Monitor mode

```
sudo ifconfig (interface) down
sudo macchanger -r (interface)
sudo ifconfig (interface) up
sudo airmon-ng start (interface)
```

Start bettercap with the interface that is now in monitor mode

```
bettercap -iface wlan0mon
```

<figure><img src="../../.gitbook/assets/image (789).png" alt=""><figcaption></figcaption></figure>

Scan for Accesspoints with `wifi.recon on`  We can also show the manufacturer of the WiFi with:

```
set wifi.show.manufacturer true
wifi.show
```

<figure><img src="../../.gitbook/assets/image (788).png" alt=""><figcaption></figcaption></figure>

If I want to see the access points in descending order of the clients connected to it:

```
set wifi.show.sort clients desc
wifi.show
```

<figure><img src="../../.gitbook/assets/image (790).png" alt=""><figcaption></figcaption></figure>

We can also sort the SSID Alphabetically:

```
set wifi.show.sort essid asc
wifi.show
```

Now lets set how many SSIDs we want to see:

```
set wifi.show.limit X
wifi.show
```
