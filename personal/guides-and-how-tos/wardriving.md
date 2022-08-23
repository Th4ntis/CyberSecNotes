# Wardriving

## About

Basic info of War driving can be found [here](../../general/networking/wireless/wardriving-wifi-sniffing.md). War driving, also known as "WiFi sniffing" is the process of locating WiFi networks, and potentially sniffing their traffic. I am running this on a RaspberryPi 4 but you can run this on any linux host. The [RaspberryPi](https://www.amazon.com/raspberry-pi-4/s?k=raspberry+pi+4) is just smaller and more portable. I run this on [Ubuntu](https://ubuntu.com/) and/or [Raspbian](https://www.raspbian.org/).

## Software

* [Kismet](https://www.kismetwireless.net/) - A powerful and popular tool made by [Dragorn](https://twitter.com/KismetWireless). "Kismet is a wireless network and device detector, sniffer, wardriving tool, and WIDS (wireless intrusion detection) framework.It works with Wi-Fi interfaces, Bluetooth interfaces, some SDR (software defined radio) hardware like the RTLSDR, and other specialized capture hardware."
  * To install kismet, follow [the guide on their docs](https://www.kismetwireless.net/docs/readme/packages/).
* [GPSD](https://en.wikipedia.org/wiki/Gpsd) - **gpsd** is a computer software program that collects data from a GPS receiver and provides the data via an IP network to potentially multiple client applications in a server-client application architecture.
  * This can be installed on most Ubuntu/Raspbian `sudo apt install gpsd gpsd-clients`

Raspbian Install (I usually go with Nightly builds):

```
wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key | sudo apt-key add -
echo 'deb https://www.kismetwireless.net/repos/apt/git/buster buster main' | sudo tee /etc/apt/sources.list.d/kismet.list
sudo apt update
sudo apt install kismet
```

Ubuntu Install (I usually go with Nightly builds):

```
wget -O - https://www.kismetwireless.net/repos/kismet-release.gpg.key | sudo apt-key add -
echo 'deb https://www.kismetwireless.net/repos/apt/git/jammy jammy main' | sudo tee /etc/apt/sources.list.d/kismet.list
sudo apt update
sudo apt install kismet
```

## Equipment

I myself have and recommend these adapters:

### WiFi Adapters

* [Alfa AWUS036ACM](https://www.amazon.com/Alfa-AWUS036ACM-Long-Range-Dual-Band-Wireless/dp/B073X6RL9D) <-- Capable of 2.4GHz and 5GHz
* [Alfa AWUS036ACHM](https://www.amazon.com/gp/product/B08SJBV1N3/ref=ox\_sc\_act\_title\_1?smid=A20G3A026MV70R\&psc=1) <-- Capable of 2.4GHz and 5GHz
* [Alfa AWUS036ACH](https://www.amazon.com/dp/B08SJC78FH?ref\_=cm\_sw\_r\_cp\_ud\_dp\_PSZZG6J9X0XH40GXB685) <-- Capable of 2.4GHz and 5GHz (This more than likely \*will\* require driver installation)

### GPS Adapters

* [GlobalSat BU-353-S4](https://www.amazon.com/GlobalSat-BU-353-S4-Receiver-Black-Improved-New/dp/B098L799NH/ref=sr\_1\_1?crid=2WAQ665IR5UV1\&keywords=GlobalSat+BU-353-S4\&qid=1660969339\&s=electronics\&sprefix=globalsat+bu-353-s4+%2Celectronics%2C148\&sr=1-1)
* [VK-162](https://www.amazon.com/dp/B01EROIUEW?ref=ppx\_pop\_mob\_ap\_share)
* [HiLetgo VK172](https://www.amazon.com/dp/B01MTU9KTF?ref=ppx\_pop\_mob\_ap\_share)

## Process

After plugging in your adapter, depending which one you have, you'll wanna set the GPSD to the proper adapter. We can run `dmesg` to find the location of the USB device. The usual locations are:

GlobatSat BU-353-S4:

```bash
/dev/ttyUSB0
```

![](<../../.gitbook/assets/image (2) (3).png>)

VK-162/VK172:

```
/dev/ttyASM0
```

![](<../../.gitbook/assets/image (13).png>)

![](<../../.gitbook/assets/image (16).png>)

With the device plugged in, set GPSD to the device, it shouldn't return an error, if it does you may need to troubleshoot the error.

```
gpsd /dev/ttyUSB0
```

OR

```
gpsd -b /dev/ttyUSB0
```

To verify if it is working properly we can run `gpsmon` OR `cgps`

![](<../../.gitbook/assets/image (7) (2).png>)

![](<../../.gitbook/assets/image (8) (2).png>)

## Running - Normal Mode

Now we can start and run kismet! We need to specify the WiFi Adapter and gps.

```
kismet -c (interface) gps=gpsd:host=localhost,port=2947,reconnect=true
```

![](<../../.gitbook/assets/image (4).png>)

![](<../../.gitbook/assets/image (14).png>)

Now as the banner at the top says, we can go to the web interface at [http://localhost:2501/](http://localhost:2501/).

![](<../../.gitbook/assets/image (3) (2).png>)

If you don't specify an interface in the original command, when on the dashboard, you can select the 3 Lines in the top left, select 'Datasources' and enable the sources you want to use.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

From here we can verify the GPS is working with the green cross hair icon in the top right, as well as seeing the info.

## Running - Wardrive Mode

If you're on the newest kismet version (2022-01-git and subsequent releases) we can run kismet in a specified [wardriving mode](https://www.kismetwireless.net/docs/readme/wardriving/).

```
kismet -t some_wardrive --override wardrive
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

and just as above, If you don't specify an interface in the original command, when on the dashboard, you can select the 3 Lines in the top left, select 'Datasources' and enable the sources you want to use.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

From here we can verify the GPS is working with the green cross hair icon in the top right, as well as seeing the info.

## Post Capture

### Normal Mode

This will automatically log all traffic to a Kismet log file with the date from the directory where the command was run.

![](<../../.gitbook/assets/image (1) (2).png>)

If we have GPS enabled and the info, we can convert the file into a KML File to be used with [Google Earth](https://earth.google.com/web/). [More info here](https://www.kismetwireless.net/docs/readme/kml/).

```bash
kismetdb_to_kml --in some-kismet-log-file.kismet --out some-kml-file.kml
```

We are able to convert the file to pcap to be analyzed in [Wireshark](../../general/attack-and-defense/wireshark.md). Docs can be found [here](https://www.kismetwireless.net/docs/readme/kismetdb\_to\_pcap/).

```
kismetdb_to_pcap --in some-kismet-log.kismet --out some-pcap-log.pcapng
```

![](<../../.gitbook/assets/image (3).png>)

We can also upload the logs to [Wigle.net](https://wigle.net/index). Docs can be found [here](https://www.kismetwireless.net/docs/readme/wigle/).

```
kismetdb_to_wiglecsv --in some-kismet-log-file.kismet --out some-wigle-file.csv
```

You can then upload it.

### Wardrive Mode

This mode will automatically create 2 files: a kismet file and a wiglecsv file to upload to [Wigle.net](https://wigle.net/index). Docs can be found [here](https://www.kismetwireless.net/docs/readme/wardriving/).

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>



If we have GPS enabled and the info, we can convert the file into a KML File to be used with [Google Earth](https://earth.google.com/web/). [More info here](https://www.kismetwireless.net/docs/readme/kml/).

```bash
kismetdb_to_kml --in some-kismet-log-file.kismet --out some-kml-file.kml
```

We are able to convert the file to pcap to be analyzed in [Wireshark](../../general/attack-and-defense/wireshark.md). Docs can be found [here](https://www.kismetwireless.net/docs/readme/kismetdb\_to\_pcap/).

```
kismetdb_to_pcap --in some-kismet-log.kismet --out some-pcap-log.pcapng
```
