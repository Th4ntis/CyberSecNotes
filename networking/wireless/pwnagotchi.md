# Pwnagotchi

The [Pwnagotchi](https://twitter.com/pwnagotchi) is an A2C-based “AI” powered by [bettercap](https://www.bettercap.org/) that learns from its surrounding WiFi environment in order to maximize the crackable WPA key material it captures (either through passive sniffing or by performing deauthentication and association attacks).

Originally created by [EvilSocket](https://github.com/evilsocket), it went unmaintained and was picked up by [Jayofelony](https://github.com/jayofelony), [aluminum-ice](https://github.com/aluminum-ice), and [WPA2](https://github.com/wpa-2) to continue development.

There is great documentation on the [new website](https://pwnagotchi.org/), as well as the [original website](https://pwnagotchi.ai/).

I am using the [RaspberryPi Imager](https://www.raspberrypi.com/software/) software with the [Jayofelony image](https://github.com/jayofelony/pwnagotchi/releases)(version 2.8.6 at the time of writing) as I am running a [RaspberyPi Zero 2W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/). If you're running on other hardware, see [the other images](https://pwnagotchi.org/3rd-party-images/index.html) and choose the one that fits your build.

For this, I will use Debian as my host operating system, but it can also be done on Windows with [PuTTY](https://putty.org/) for SSH and [7-Zip](https://7-zip.org/) for extracting the image; you may also need RNDIS drivers from ModCloud, which can be obtained [here](https://modclouddownloadprod.blob.core.windows.net/shared/mod-rndis-driver-windows.zip). I won't cover the Windows path here, but feel free to reach out if you'd like.

### Flashing

After the image is downloaded, extract it so you have a `.img` file.

<figure><img src="../../.gitbook/assets/image (298).png" alt=""><figcaption></figcaption></figure>

Open the Raspberry Pi Imager and choose your device. As I am using a Pi Zero 2W, I will select that.

<figure><img src="../../.gitbook/assets/image (355).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (388).png" alt=""><figcaption></figcaption></figure>

Then choose the image you want. We will scroll to the bottom and select `CUSTOM IMAGE` and choose our .img we extracted.

<figure><img src="../../.gitbook/assets/image (413).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (473).png" alt=""><figcaption></figcaption></figure>

Choose the MicroSD card you have inserted.

<figure><img src="../../.gitbook/assets/image (482).png" alt=""><figcaption></figcaption></figure>

When asked if you would like to apply OS customisation, choose `No`.

<figure><img src="../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

It will inform you that the entire SD card will be erased and ask if that is OK. Choose yes.

<figure><img src="../../.gitbook/assets/image (536).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (582).png" alt=""><figcaption></figcaption></figure>

Once it's done flashing, you're good to plug the Micro SD card into your Pi!

<figure><img src="../../.gitbook/assets/image (584).png" alt=""><figcaption></figcaption></figure>

### Starting

Start by connecting the micro-USB cable to the data port of your Pwnagotchi’s RPi, then connect the other end of that cable to your computer.

<figure><img src="../../.gitbook/assets/image (654).png" alt=""><figcaption></figcaption></figure>

* If your Pwnagotchi has already been booted up at least once before, you will soon see a new Ethernet interface on your host computer.
* If you have never booted your Pwnagotchi before, it will take a few minutes to boot and become visible or responsive. **DO NOT INTERRUPT YOUR PWNAGOTCHI DURING THIS PROCESS.** Just give it time to do its thing; I recommend \~10 minutes.

When you see a new Ethernet interface on your host computer, you’ll need to configure it with a static IP address of:

```
IP: 10.0.0.1
Netmask: 255.255.255.0
Gateway: 10.0.0.1
DNS (if required): 8.8.8.8 (or whatever)
```

<figure><img src="../../.gitbook/assets/image (671).png" alt=""><figcaption></figcaption></figure>

If everything’s been configured properly, you will now be able to ping either `10.0.0.2` or `pwnagotchi.local`. If we are able to ping the Pi, we should now be able to connect to your unit using SSH:

```
ssh pi@10.0.0.2
```

<figure><img src="../../.gitbook/assets/image (684).png" alt=""><figcaption></figcaption></figure>

With this plugged into your computer, you can go to the pwnagotchi UI at http://10.0.0.2:8080 to see it's face in manual mode. The default username and password is `changeme:changeme`

<figure><img src="../../.gitbook/assets/image (691).png" alt=""><figcaption></figcaption></figure>

## Config

We can copy the default config file and edit that, so we know what formatting to use. I find this easier, but you can also copy/paste individual settings or start from scratch. To copy the default config we run:

```
sudo cp /etc/pwnagotchi/default.toml /etc/pwnagotchi/config.toml
```

The config lives at `/etc/pwnagotchi/config.toml`. To edit it we run:

```
sudo nano /etc/pwnagotchi/config.toml
```

With this open we can modify many settings, such as the name, the networks to whitelist (ignore), the default Web UI login, and plugin settings.

<figure><img src="../../.gitbook/assets/image (703).png" alt=""><figcaption></figcaption></figure>

### Plugins

There's a variety of cool plugins we can use, such as Bluetooth pairing so we can access the pwnagotchi fom our phone, uploading to websites, and more. There's some [3rd Party plugins](https://pwnagotchi.org/3rd-party-plugins/index.html) as well.

<figure><img src="../../.gitbook/assets/image (723).png" alt=""><figcaption></figcaption></figure>

I like to use the bluetooth so I can access it from my phone while out with it, but that isn't necessary.

### Bluetooth

Our pwnagotchi will indicate the status via a little BT symbol at the top of the screen. The status codes are:

* C Connected: This means the connection to the device has been established.
* NF Not found: This means the connection to the device could not be established (probably because it could not be found).
* PE Pairing Error: This error occurs on a pairing problem.
* BE Bnep Error: This error occurs, when the NAP could not be created.
* AE Address Error: The IP could not be assigned to the NAP interface.

#### Setup

To set this up, we find the section in the config file for our phone's Bluetooth MAC address. Which section you use depends on whether you're on iPhone or Android, and it is straightforward once you read it.

<figure><img src="../../.gitbook/assets/image (749).png" alt=""><figcaption></figcaption></figure>

After we save the setting and put it into Auto mode via the web UI, make your device discoverable via bluetooth, and it should attempt to pair/connect with your phone.

<figure><img src="../../.gitbook/assets/image (752).png" alt=""><figcaption></figcaption></figure>

If it does not try to connect after a couple of minutes, we may need to manually pair the devices. To do this, put your phone in discoverable mode. On the pwnagotchi, run:

```
sudo bluetoothctl
```

and once in the bluetooth-shell, to scan for nearby bluetooth devices, run

```
scan on
```

When you see the name/mac address of your phone run:

```
pair <mac>
```

and

```
trust <mac>
```

We will soon be prompted on the phone to allow connection from our pwnagotchi hostname.

Once we pair and trust the device, we can see we're connected!

<figure><img src="../../.gitbook/assets/image (780).png" alt=""><figcaption></figcaption></figure>

## Conclusion

With that, we've got a pwnagotchi set up and connected via Bluetooth. From here, experiment with other plugins, and add a [Waveshare screen](https://www.waveshare.com/product/raspberry-pi/displays/2.13inch-e-paper-hat-g.htm) and a [PiSugar battery](https://www.pisugar.com/) to make it even more portable. You can even customize it with [Fancygotchi](https://github.com/Pwnagotchi-Unofficial/pwnagotchi-fancygotchi), though note that is for images other than Jayofelony's, which I am using here.
