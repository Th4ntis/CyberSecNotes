# 🥥 WiFi Coconut

## About

The [Hak5 WiFi Coconut](https://shop.hak5.org/products/wifi-coconut) captures standard PCAP files with its 14 finely tuned 802.11 WiFi radios, and integrates with popular tools like Kismet & Wireshark. There are 14 channels on the 2.4 GHz WiFi spectrum. It is an Open source full-spectrum WiFi sniffer that simultaneously monitors the entire 2.4 GHz airspace.

### Links

[Store Page](https://shop.hak5.org/products/wifi-coconut)&#x20;

[Doumentation](https://docs.hak5.org/wifi-coconut/wifi-coconut-by-hak5/)

## Setup / Installing

```bash
sudo apt install build-essential cmake libusb-1.0-0-dev libpcap-dev git
git clone https://github.com/hak5/hak5-wifi-coconut && cd hak5-wifi-coconut
mkdir build && cd build
cmake ../
make
make install
```

## Running

```bash
sudo wifi_coconut
```

## Running with other tools

### TCPDump

```bash
sudo wifi_coconut --no-display --pcap=- | tcpdump -r -
```

### TShark

```bash
sudo wifi_coconut --no-display --pcap=- | tshark -r -
```

### Kismet

Kismet integrates a WiFi Coconut capture tool as of **2022-08-11-nightly** More info on the Coconut and Kismet can be found [here](https://docs.hak5.org/wifi-coconut/capture-files/kismet/).

```none
sudo apt install -y kismet-capture-hak5-wifi-coconut
```

* View coconuts that are connected

```
kismet_cap_hak5_wifi_coconut --list
```

* Running with the coconut

```none
kismet -c coconut:name=WifiCoconut
```
