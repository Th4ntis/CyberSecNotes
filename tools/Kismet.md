# About
Kismet is a wireless network and device detector, sniffer, wardriving tool, and WIDS (wireless intrusion detection) framework.

Kismet works with Wi-Fi interfaces, Bluetooth interfaces, some SDR (software defined radio) hardware like the RTLSDR, and other specialized capture hardware.
## Links
[Kismet Homepage](https://www.kismetwireless.net/)
[Kismet Github](https://github.com/kismetwireless/kismet)
# Install
You can follow their documentation page [here](https://www.kismetwireless.net/docs/readme/quickstart/) and [here](https://www.kismetwireless.net/docs/readme/packages/). I install it on ubuntu 20.04 with:
- Install Pre Reqs
```
sudo apt install -y build-essential git libwebsockets-dev pkg-config zlib1g-dev libnl-3-dev libnl-genl-3-dev libcap-dev libpcap-dev libnm-dev libdw-dev libsqlite3-dev libprotobuf-dev libprotobuf-c-dev protobuf-compiler protobuf-c-compiler libsensors4-dev libusb-1.0-0-dev python3 python3-setuptools python3-protobuf python3-requests python3-numpy python3-serial python3-usb python3-dev python3-websockets librtlsdr0 libubertooth-dev libbtbb-dev
```

- Remove older versions of Kismet
```
sudo rm -rfv /usr/local/bin/kismet* /usr/local/share/kismet* /usr/local/etc/kismet*
```

- Add the APT key
```
wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key | sudo apt-key add -
```

```
echo 'deb https://www.kismetwireless.net/repos/apt/release/focal focal main' | sudo tee /etc/apt/sources.list.d/kismet.list
```

- Update repos and install kismet
```
sudo apt update && sudo apt install -y kismet
```

- Add current user to the Kismet group
```
sudo usermod -aG kismet $USER
```

This install dependencies that are required by kismet, removes any other/old instances of kismet, gets the gpg key and adds the source to the ubuntu source repositories, updates our source repositories so it knows where to obtain the most recent kismet from. Installs kismet and adds the user we currently are to the kismet group.

# Usage

Running `kismet` will start a local webserver for you to access via a web browser via http://localhost:2501. You can then set your login information there.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FJ4JurAjpNe18SxV3cMY2%252Fimage.png%3Falt%3Dmedia%26token%3D1db5c8e7-9f0c-4632-a43e-07678d2ba52c&width=768&dpr=4&quality=100&sign=a544d3a3&sv=2)

From here we can specify and interface, bluetooth device, and/or GPS adapter to use. These options can also be set when starting kismet via the command line or choosing the defaults by editing the `kismet.conf` file in `/etc/kismet/kismet.conf`.