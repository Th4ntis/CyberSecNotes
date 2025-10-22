# About
Bettercap is "The Swiss Army knife for [WiFi](https://www.bettercap.org/modules/wifi/), [Bluetooth Low Energy](https://www.bettercap.org/modules/ble/), wireless [HID hijacking](https://www.bettercap.org/modules/hid/) and [IPv4 and IPv6](https://www.bettercap.org/modules/ethernet) networks reconnaissance and MITM attacks."
## Links
[Bettercap Homepage](https://www.bettercap.org/)
[Bettercap Github](https://github.com/bettercap/bettercap)
# Install
There's multiple ways to install bettercap, they have documentation [here](https://www.bettercap.org/installation/). I typically install from source. Currently having [Go installed](https://go.dev/doc/install).
```
go install github.com/bettercap/bettercap@latest
```

```
sudo ~/.go/bin/bettercap -eval "caplets.update; ui.update; q"
```
# Usage
Running `bettercap` in the terminal will allow you to run bettercap via the commandline and will be met with the bettercap prompt. Edit the default credentials for the web interface at `/usr/local/share/bettercap/caplets/http-ui.cap` and/or `/usr/local/share/bettercap/caplets/http-ui.cap`. You can also run via the web interface via `sudo bettercap -caplet http-ui` OR `sudo bettercap -caplet https-ui`. Then you can go to [http://127.0.0.1/](http://127.0.0.1/) OR [https://127.0.0.1/](http://127.0.0.1/).

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FPX5s3FRkDGrXUfJuD3wI%252Fimage.png%3Falt%3Dmedia%26token%3Dde6f4743-d404-42e5-98d2-9f76784deba2&width=768&dpr=4&quality=100&sign=606a575&sv=2)
## Command Line
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

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FPuxgT9w0nILOf0xlcJWD%252Fimage.png%3Falt%3Dmedia%26token%3D7ada8673-fea5-4047-9a72-8b0093324593&width=768&dpr=4&quality=100&sign=5b3f3630&sv=2)

Scan for Accesspoints with `wifi.recon on` We can also show the manufacturer of the WiFi with:
```
set wifi.show.manufacturer true
wifi.show
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F9pHeKRw9VCM3niTJkkD3%252Fimage.png%3Falt%3Dmedia%26token%3D807d710a-b4b4-4549-aaf7-a48a830248b7&width=768&dpr=4&quality=100&sign=6133608d&sv=2)

If I want to see the access points in descending order of the clients connected to it:
```
set wifi.show.sort clients desc
wifi.show
```

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FxWp7MfC4g62u1URzRexV%252Fimage.png%3Falt%3Dmedia%26token%3D9f89fbb4-1b70-46bb-a604-3e1150de30a5&width=768&dpr=4&quality=100&sign=cd98b46b&sv=2)

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