# Pwnagotchi

## Pwnagotchi

The [Pwnagotchi](https://twitter.com/pwnagotchi) is an A2C-based “AI” powered by [bettercap](https://www.bettercap.org/) that learns from its surrounding WiFi environment in order to maximize the crackable WPA key material it captures (either through passive sniffing or by performing deauthentication and association attacks).

Originally created by [EvilSocket](https://github.com/evilsocket), it was not maintained and was picked up by [Jayofelony](https://github.com/jayofelony), [Aliminum-Ice](https://github.com/aluminum-ice), and [WPA2](https://github.com/wpa-2) to continue development.

There is great document on the [new website](https://pwnagotchi.org/), as well as the [original website](https://pwnagotchi.ai/).

I am using the [RaspberryPi Imager](https://www.raspberrypi.com/software/) software with the [Jayofelony image](https://github.com/jayofelony/pwnagotchi/releases)(version 2.8.6 at the time of writing) as I am running a [RaspberyPi Zero 2W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/). If you're running on other hardware, see [the other images](https://pwnagotchi.org/3rd-party-images/index.html) and choose the one that fits your build.

For this, I will be using Debian as my host machine operating system, but this can also be done on Windows with the [Putty software](https://putty.org/) for SSH, [7Zip](https://7-zip.org/) for extracting the image, and you may need RNDIS drivers from ModCloud which can obtained [here](https://modclouddownloadprod.blob.core.windows.net/shared/mod-rndis-driver-windows.zip). I will not be covering those in here but feel fre to reach out if you would like.

## Flashing

After the image is downloaded, extract it so you have a `.img` file.

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/16201579-e6e3-49d2-809b-b63627df49c4)

Open the RaspberryPi Imager and choose your device. As I am using a Pi Zero 2W, I will be selecing that. &#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/a543b0f8-1654-4b68-8e16-6b0782472846" alt=""><figcaption></figcaption></figure>

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/fbab3173-3041-4c5c-9f3b-33f7190ee96c" alt=""><figcaption></figcaption></figure>

Then choose the image you want. We will scroll to the bottom and select `CUSTOM IMAGE` and choose our .img we extracted. &#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/67e10c3d-b0d6-4ef8-b620-f93b27d62212" alt=""><figcaption></figcaption></figure>

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/9d3a7832-62d1-46bb-989e-52651a11b52f" alt=""><figcaption></figcaption></figure>

Choose the MicroSD card you have inserted.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/87117a04-347b-4529-9a7e-b3de883bb213" alt=""><figcaption></figcaption></figure>

When asked if you would like to apply OS customisation, choose `No`.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/edd55e38-7b09-4538-8b57-8f711e51ea1d" alt=""><figcaption></figcaption></figure>

It will inform you that the entire SD card will be erased and ask if that is OK. Choose yes. &#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/2e886a8b-83b8-4b79-b0d2-fd05521bb829" alt=""><figcaption></figcaption></figure>

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/507a6dfd-b0b4-490f-b08f-86bef7322870" alt=""><figcaption></figcaption></figure>

Once it's done flashing, you're good to plug the Micro SD card into your Pi!&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/7b74f2cb-a16f-493c-b4a3-6b2019fd9f5c" alt=""><figcaption></figcaption></figure>

## Starting

Start by connecting the micro-USB cable to the data port of your Pwnagotchi’s RPi, then connect the other end of that cable to your computer.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/77eeb85d-d7c8-4c31-834e-4deb266b5228" alt=""><figcaption></figcaption></figure>

* If your Pwnagotchi has already been booted up at least once before, you will soon see a new Ethernet interface on your host computer.
* If you have never booted your Pwnagotchi before, it will take a few minutes to boot up or become visible or responsive. **DO NOT INTERRUPT YOUR PWNAGOTCHI DURING THIS PROCESS**. Just give it time to do it's thing, I recommend \~10 minutes.

When you see a new Ethernet interface on your host computer, you’ll need to configure it with a static IP address of:

```
IP: 10.0.0.1
Netmask: 255.255.255.0
Gateway: 10.0.0.1
DNS (if required): 8.8.8.8 (or whatever)
```

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/c1e2cd10-f742-4f3d-9002-3ff6b8afe41a)

If everything’s been configured properly, you will now be able to ping either `10.0.0.2` or `pwnagotchi.local`. If we are able to ping the Pi, we should now be able to connect to your unit using SSH:

```
ssh pi@10.0.0.2
```

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/be7f197b-3b9f-4e59-86a7-bbc4b6d0a52a)

With this plugged into your computer, you can go to the pwnagotchi UI at http://10.0.0.2:8080 to see it's face in manual mode. The default username and password is `changeme:changeme`&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/0ff6e1a9-9589-4fd1-a431-a8c6c9488afc" alt=""><figcaption></figcaption></figure>

## Config

We can copy the default config file and make edits to that so we know what formatting and such to use. I find this easier but you can also just copy/paste settings or start on your own. To copy the default config we run:

```
sudo cp /etc/pwnagotchi/default.toml /etc/pwnagotchi/config.tml
```

The config location is `/etc/pwnagotchi/config.yml` , to edit this we can run

```
sudo nano /etc/pwnagotchi/config.yml
```

With this open we can modify multiple settings, like the name, WiFi's to whitelist(ignore), the default Web UI login, and plugin settings.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/882095a0-b64c-49b1-ba9a-d7611cb4f6f0" alt=""><figcaption></figcaption></figure>

## Plugins

There's a variety of cool plugins we can use, such as Bluetooth pairing so we can access the pwnagotchi fom our phone, uploading to websites, and more. There's some [3rd Party plugins](https://pwnagotchi.org/3rd-party-plugins/index.html) as well.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/40475fb3-02e4-44a9-b842-2458d4fce0f8" alt=""><figcaption></figcaption></figure>

I like to use the bluetooth so I can access it from my phone while out with it, but that isn't necessary.

### Bluetooth

Our pwnagotchi will indicate the status via a little BT symbol at the top of the screen. The status codes are:

* C Connected: This means the connection to the device has been established.
* NF Not found: This means the connection to the device could not be established (probably because it could not be found).
* PE Pairing Error: This error occurs on a pairing problem.
* BE Bnep Error: This error occurs, when the NAP could not be created.
* AE Address Error: The IP could not be assigned to the NAP interface.

#### Setup

To set this up, in the config file, we find a section to add in our phones bluetooth mac address. Depending on if you're using iPhone or Android will determine which section you use. It's straight forward when reading it.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/ab2f75a7-7fd0-41fe-9b7b-464fb159c818" alt=""><figcaption></figcaption></figure>

After we save the setting and put it into Auto mode via the web UI, make your device discoverable via bluetooth, and it should attempt to pair/connect with your phone.&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/a2a1496d-31da-47e9-9e93-ed0298215053" alt=""><figcaption></figcaption></figure>

If this does not try to connect after a couple mintes, we may need to manually pair our devices together. To do this, put your phone in discoverable mode. On our pwnagotchi, run

```
sudo bluetoothctl
```

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/8faa1f33-f7ad-460e-ac0e-70ae1cc1a278)

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

Once we pair and trust the device, we can see we're connected!&#x20;

<figure><img src="https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/1b857ddb-6850-4eb0-8d18-fd95efec0eae" alt=""><figcaption></figcaption></figure>

## Conclusion

With that, we've got a pwnagotchi setup and connected via Bluetooth. From here, experiment with other plugins, get a nice [waveshare sceen](https://www.waveshare.com/product/raspberry-pi/displays/2.13inch-e-paper-hat-g.htm) and [PiSugar battery](https://www.pisugar.com/) to make it even more portable! Even checkout ways to cusomize it with [Fancygotchi](https://github.com/Pwnagotchi-Unofficial/pwnagotchi-fancygotchi) if you're not using Jayofelonys image like I am.
