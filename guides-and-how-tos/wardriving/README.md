# Wardriving

## About

Wardriving, also known as "WiFi sniffing" is the process of locating WiFi networks, and potentially sniffing their traffic. War driving involves searching for wireless networks with vulnerabilities while moving around an area in various methods such as driving, walking, or biking. They use hardware and software to discover unsecured WiFi networks then can gain unauthorized access to the network by cracking WiFi passwords. Then records vulnerable network locations on digital maps, known as access point mapping, and may share that information with third-party applications or websites.

As mentioned before this is able to detect unsecured WiFi traffic. So when you're connected to an open public WiFi, sniffing is able to capture and log the traffic between your machine and the access point, and potentially capture unsecured credentials when logging into an insecure website, or gather encrypted traffic to attempt to decrypt later.

In some cases, a method of war driving is also capturing encrypted WiFi passwords in the form of a Handshake or a PMKid, using methods and tools like aircracl or hcxdumpttool, to then crack later and connect to later.

### Methods

There's multiple ways of war driving, using your laptop a [Raspberry Pi](https://www.raspberrypi.com/) with appropriate devices such as [GPS adapters](https://www.amazon.com/gp/product/B01EROIUEW/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8\&psc=1), [antennas](https://www.amazon.com/gp/product/B08SJBV1N3/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8\&psc=1), or even your phone with the [WiGLE WiFi app](https://play.google.com/store/apps/details?id=net.wigle.wigleandroid\&utm_source=global_co\&utm_medium=prtnr\&utm_content=Mar2515\&utm_campaign=PartBadge\&pcampaignid=MKT-AC-global-none-all-co-pr-py-PartBadges-Oct1515-1). Popular softwares include Wireshark, Kismet, or use specified devices such as the [WiFi Coconut](https://hakshop.com/products/wifi-coconut) from [Hak5](https://hak5.org/pages/about).

### Is this legal?

This is a bit of a grey area in some cases/areas and depending what you doing, weather you're just scanning networks and nothing more, or attempting to gather WiFi hashes. Typically this is not as it's just collecting basic public information, such as the WiFi name(BSSID), the security(WPA, WPA2, etc), and location(using GPS). This isn't inherently malicious or nefarious but it _could_ be used that way by those with malicious intent.

***

I am running this on a RaspberryPi 4 and/or a Debian 13 Laptop.

## Hardware

* Laptop - Running [Debian](https://www.debian.org/distrib/?pubDate=20250809) or [Kali Linux](https://www.kali.org/get-kali/#kali-platforms)
* [RaspberryPi](https://www.raspberrypi.com/) (I use a 3B+ and a 4) **OR** [Zimaboard](https://www.zimaboard.com/) running [Ubuntu Server](https://ubuntu.com/server)

I have and recommend the following:

## WiFi Adapters

* [Alfa AWUS036ACM](https://www.amazon.com/Alfa-AWUS036ACM-Long-Range-Dual-Band-Wireless/dp/B073X6RL9D) <-- Capable of 2.4GHz and 5GHz
* [Alfa AWUS036ACHM](https://www.amazon.com/gp/product/B08SJBV1N3/ref=ox_sc_act_title_1?smid=A20G3A026MV70R\&psc=1) <-- Capable of 2.4GHz and 5GHz
* [Alfa AWUS036ACH](https://www.amazon.com/dp/B08SJC78FH?ref_=cm_sw_r_cp_ud_dp_PSZZG6J9X0XH40GXB685) <-- Capable of 2.4GHz and 5GHz (This more than likely \*will\* require driver installation)
* [WiFi Coconut](https://shop.hak5.org/collections/wifi-pentesting/products/wifi-coconut) <-- Capable of only 2.4GHz BUT has 14 integrated WiFi radios so you can be on all channels, all the time.

## GPS Adapters

* [GlobalSat BU-353-S4](https://www.amazon.com/GlobalSat-BU-353-S4-Receiver-Black-Improved-New/dp/B098L799NH/ref=sr_1_1?crid=2WAQ665IR5UV1\&keywords=GlobalSat+BU-353-S4\&qid=1660969339\&s=electronics\&sprefix=globalsat+bu-353-s4+%2Celectronics%2C148\&sr=1-1)
* [VK-162](https://www.amazon.com/dp/B01EROIUEW?ref=ppx_pop_mob_ap_share)
* [HiLetgo VK172](https://www.amazon.com/dp/B01MTU9KTF?ref=ppx_pop_mob_ap_share)

## Software

* [Kismet](https://www.kismetwireless.net/) - A powerful and popular tool made by [Dragorn](https://twitter.com/KismetWireless). "Kismet is a wireless network and device detector, sniffer, wardriving tool, and WIDS (wireless intrusion detection) framework.It works with Wi-Fi interfaces, Bluetooth interfaces, some SDR (software defined radio) hardware like the RTLSDR, and other specialized capture hardware."
  * To install kismet, follow [the guide on their docs](https://www.kismetwireless.net/packages/#kali).
  * Kismet Config files readme can be found [here](https://www.kismetwireless.net/docs/readme/configuring/configfiles/).
  * Kismet wardriving overlay docs can be found [here](https://www.kismetwireless.net/docs/readme/configuring/wardrive/).
* [GPSD](https://en.wikipedia.org/wiki/Gpsd) - **gpsd** is a computer software program that collects data from a GPS receiver and provides the data via an IP network to potentially multiple client applications in a server-client application architecture.
  * This can be installed on most Ubuntu/Raspbian `sudo apt install gpsd gpsd-clients`
* Debian Trixies (13)

```
wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key --quiet | gpg --dearmor | sudo tee /usr/share/keyrings/kismet-archive-keyring.gpg >/dev/null
echo 'deb [signed-by=/usr/share/keyrings/kismet-archive-keyring.gpg] https://www.kismetwireless.net/repos/apt/release/trixie trixie main' | sudo tee /etc/apt/sources.list.d/kismet.list >/dev/null
sudo apt update
sudo apt install kismet
```

* Kali

```
wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key --quiet | gpg --dearmor | sudo tee /usr/share/keyrings/kismet-archive-keyring.gpg >/dev/null
echo 'deb [signed-by=/usr/share/keyrings/kismet-archive-keyring.gpg] https://www.kismetwireless.net/repos/apt/release/kali kali main' | sudo tee /etc/apt/sources.list.d/kismet.list >/dev/null
sudo apt update
sudo apt install kismet
```

* Raspbian Install (I usually go with Nightly builds):

```bash
git clone https://www.kismetwireless.net/git/kismet.git && cd kismet
./configure
make
make -j$(nproc)
sudo make suidinstall
sudo usermod -aG kismet $USER
```

## Setup (RPi)

### kismet\_site.conf file

As long as you have a large enough MicroSD the Pi is running on, you _**should**_ be fine BUT if you would like to use an external HDD or USB Drive for storage, we need to set that to automount.

Verify the drive you want mounted with: `df -h` and verify where it's mount location.

We need to find the UUID of the Drive we mounted, most likely will be `/dev/sda1` but not always the case, so be sure to verify. Find the UUID with:

```
sudo blkid /dev/sda1
```

!\[\[image 180.png]]

We need to create a directory for this to me auto mounted on boot:

```
sudo mkdir -p /mnt/usb1
```

Now change the ower of the newly made directory (changing th4ntis with your username):

```
sudo chown -R th4ntis:th4ntis /mnt/usb1
```

To set this to auto mount on startup I edited my `/etc/fstab` with:

```
sudo nano /etc/fstab
```

Then added this to the bottom of the file:

```
UUID=[UUID] /mnt/usb1 [TYPE] defaults,auto,users,rw,nofail,noatime 0 0
```

changing the \[UUID] and \[TYPE] to the UUID and type of your drive when we used `sudo blkid /dev/sda1`. !\[\[image 181.png]]

We have a couple options, we can edit the kismet.conf file OR use the kismet\_site.conf file. I chose the kismet\_site.conf file.

Edit the file:

```
sudo nano /etc/kismet/kismet_site.conf
```

I changed the log location to the external HDD or USb Drive location: as well as added the wiglecsv format for logging to upload

```
# Changes log location
log_prefix=/dev/usb1

# Turn on wiglecsv format
log_types+=wiglecsv
```

## Setup Cont.

Now we need to add the WiFi Radios, GPS, and Bluetooth sources to the kismet\_site.conf

After plugging in your WiFi Radios, GPS, and Bluetooth adapters, depending which one you have, you'll wanna set the GPSD to the proper adapter. We can run `dmesg` to find the location of the USB device. The usual locations are:

### WiFi Radios:

Let's get the radio 'names' with: `ip a`

!\[\[image 182.png]]

As I am using a WiFi Coconut, I will be having a lot of WiFi Radios. So take the WiFi interface name, eg. `wlx0cefafd1408b`, and copy as many of them as you have/will be using. Then we will edit the `kismet_site.conf` file and add the sources to that. !\[\[image 183.png]]

### GPS:

GlobatSat BU-353-S4:

```bash
/dev/ttyUSB0
```

!\[\[image 184.png]]

VK-162/VK172:

```
/dev/ttyASM0
```

!\[\[image 185.png]]

With the device plugged in, set GPSD to the device, it shouldn't return an error, if it does you may need to troubleshoot the error.

```
gpsd /dev/ttyUSB0
```

OR

```
gpsd -b /dev/ttyUSB0
```

To verify if it is working properly we can run `gpsmon` **OR** `cgps` !\[\[image 187.png]]

!\[\[image 188.png]]

Now, in our kismet\_site.conf, we will add GPSD as a GPS source.

!\[\[image 189.png]]

## Running - Normal Mode

Now we can start and run kismet! We need to specify the WiFi Adapter and gps.

```
kismet -c (interface) gps=gpsd:host=localhost,port=2947,reconnect=true
```

!\[\[image 190.png]]

!\[\[image 191.png]]

Now as the banner at the top says, we can go to the web interface at [http://localhost:2501/](http://localhost:2501/).

!\[\[image 15.avif]]

If you don't specify an interface in the original command, when on the dashboard, you can select the 3 Lines in the top left, select 'Datasources' and enable the sources you want to use.

!\[\[image 192.png]]

!\[\[image 193.png]]

From here we can verify the GPS is working with the green cross hair icon in the top right, as well as seeing the info.

## Running - Wardrive Mode

If you're on the newest kismet version (2022-01-git and subsequent releases) we can run kismet in a specified [wardriving mode](https://www.kismetwireless.net/docs/readme/wardriving/).

```
kismet -t some_wardrive --override wardrive
```

!\[\[image 194.png]]

!\[\[image 195.png]]

and just as above, If you don't specify an interface in the original command, when on the dashboard, you can select the 3 Lines in the top left, select 'Datasources' and enable the sources you want to use.

!\[\[image 196.png]]

!\[\[image 197.png]]

From here we can verify the GPS is working with the green cross hair icon in the top right, as well as seeing the info.

## Autostarting Kismet

The README for starting Kismet at launch can be found [here on their github](https://github.com/kismetwireless/kismet/blob/master/packaging/systemd/README).

As I installed Kismet from the package, the service for systemd is already there.

```
By default, the Kismet systemd service runs Kismet as root; this is NOT best practices
    but it is the only user consistently available.

    It is STONGLY recommended that you install Kismet as suid-root via `make suidinstall`,
    and that you run Kismet as a non-privileged user.  Kismet will then limit root 
    access to the capture binaries which control individual interfaces.
```

So lets set this up to run as our user. `sudo systemctl edit kismet` so edit the service. Changing the user to the 'kismet' user **OR** as the user you have setup.

!\[\[image 198.png]]

So with this setup, let's start the service with `sudo service kismet start`.

Set the service to start on boot with: `sudo systemctl enable kismet`.

Verify the Kismet service is running with: `sudo service kismet status`.

!\[\[image 199.png]]

## Post Capture

### Normal Mode

This will automatically log all traffic to a Kismet log file with the date from the directory where the command was run. !\[\[image 200.png]]

If we have GPS enabled and the info, we can convert the file into a KML File to be used with [Google Earth](https://earth.google.com/web/). [More info here](https://www.kismetwireless.net/docs/readme/kml/).

```bash
kismetdb_to_kml --in some-kismet-log-file.kismet --out some-kml-file.kml
```

We are able to convert the file to pcap to be analyzed in Wireshark. Docs can be found [here](https://www.kismetwireless.net/docs/readme/kismetdb_to_pcap/).

```
kismetdb_to_pcap --in some-kismet-log.kismet --out some-pcap-log.pcapng
```

!\[\[image 201.png]]

We can also upload the logs to [Wigle.net](https://wigle.net/index). Docs can be found [here](https://www.kismetwireless.net/docs/readme/wigle/).

```
kismetdb_to_wiglecsv --in some-kismet-log-file.kismet --out some-wigle-file.csv
```

You can then upload it.

### Wardrive Mode

This mode will automatically create 2 files: a kismet file and a wiglecsv file to upload to [Wigle.net](https://wigle.net/index). Docs can be found [here](https://www.kismetwireless.net/docs/readme/wardriving/). This will sho that logging is greately reduced and will only be used for Access Point(AP) collection.

```
kismet --override wardrive
```

!\[\[image 202.png]]

If we have GPS enabled and the info, we can convert the file into a KML File to be used with [Google Earth](https://earth.google.com/web/). [More info here](https://www.kismetwireless.net/docs/readme/kml/).

```bash
kismetdb_to_kml --in some-kismet-log-file.kismet --out some-kml-file.kml
```

We are able to convert the file to pcap to be analyzed in Wireshark. Docs can be found [here](https://www.kismetwireless.net/docs/readme/kismetdb_to_pcap/).

```
kismetdb_to_pcap --in some-kismet-log.kismet --out some-pcap-log.pcapng
```
