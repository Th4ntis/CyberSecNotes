# Wifite

## About

[Wifite](https://github.com/kimocoder/wifite2) is a tool written in python used for pentesting wireless networks.

### Installing

Install prerequisites

```bash
git clone https://github.com/kimocoder/wifite2.git
cd wifite2 && pip3 install -r requirements.txt
```

### Running and installing to system

To run wifite without installing, run it from the repository

```bash
sudo ./wifite.py
```

To install it to the system

```bash
sudo python3 setup.py install
```

## Usage

To show various types of attacks and arguments we can use

```bash
sudo wifite -h
```

We can specify a wireless interface with

```
sudo wifite -i (interface)
```

OR if we only have one WiFi interface on that is capable of monitor mode, we can just run it as is.

### WPA

We can do a WPA attack on a target network with

```
sudo wifite --wpa
```

This will enable monitor mode on the wireless interface and begin scanning for networks.

I will target Pixel7, number 2

<figure><img src="../../../.gitbook/assets/image (472).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure>

This starts with a PMKID attack, then moves onto a WPA Handshake attack if a PMKID is unable to be obtained.&#x20;

<figure><img src="../../../.gitbook/assets/image (474).png" alt=""><figcaption></figcaption></figure>

\*Note, we can skip the PMKID attack by adding the argument `--no-pmkid`&#x20;

<figure><img src="../../../.gitbook/assets/image (475).png" alt=""><figcaption></figcaption></figure>

When obtaining a WPA handshake attack, this will attempt to de-authenticate clients from the network until we have obtained the handshake.

When the handshake is captured we see where it was saved to with the name of it. It will attempt to crack it automatically with `aircrack-ng` using their default worldlist `wordlist-probably.txt`&#x20;

<figure><img src="../../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

If you would like to use your own dictionary, such as `rockyou.txt` we can use the `--dict` argument.

<figure><img src="../../../.gitbook/assets/image (477).png" alt=""><figcaption></figcaption></figure>
