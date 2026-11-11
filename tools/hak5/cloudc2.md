# ☁️ CloudC2

## About

Cloud C² makes it easy for pentesters and security teams to deploy and manage Hak5 gear from the cloud.

### Links

[Product Page](https://shop.hak5.org/products/c2)

[Docs](https://docs.hak5.org/cloud-c2/cloud-c-by-hak5/)

[Downloads](https://downloads.hak5.org/cloudc2)

#### Videos

[Easy Cloud C2 Setup](https://youtu.be/TIpx_ENurLY)

[SSL with LetsEncrypt CLoudC2](https://youtu.be/cvFMf9BQLAI)

[Enabling C2 on Boot](https://youtu.be/rgmL75ZBfSI)

## Setup

To prepare for the C2 setup and install, we want to **allow** ports 22, 80, 443, and 8080 to our machine. Once that is enabled, we want to change the UFW rules as well

```
sudo ufw allow 22
sudo ufw allow 80
sudo ufw allow 443
sudo ufw allow 2022
sudo ufw allow 8080
sudo ufw enable
```

Now we also need to install unzip as it is not installed by default.

```
sudo apt install -y unzip
```

Once done, we can run this::

```
wget https://downloads.hak5.org/api/devices/cloudc2/firmwares/latest -q -O c2.zip && unzip -qq c2.zip && \
IP=$(curl -s https://checkip.amazonaws.com) && \
echo "Copy the below setup token and browse to http://$IP:8080" && \
./c2-*_amd64_linux -hostname $IP
```

Browse to the IP given !\[\[Pasted image 20260216112819.png]]

You will be prompted to give your license, setup a username, password, etc.

Once done, before adding any devices, stop the command and enable HTTPS with either a domain name OR IP.

* DOMAIN

```none
sudo ./c2-3.5.2_i386_linux -hostname DOMAIN -https
```

* IP Address

```none
sudo ./c2-3.5.2_i386_linux -hostname IP -https
```

!\[\[Pasted image 20260216113130.png]]

Once that is done, stop it and enable it as a service so it start if the machine reboots. Copy the Cloud C2 binary.

```
sudo cp c2-3.5.2_i386_linux /usr/local/bin
```

Create directory for database file

```
sudo mkdir /var/cloudc2
```

Copy the database file

```
sudo cp c2.db /var/cloudc2/
```

Create the systemd service file.

```
sudo nano /etc/systemd/system/cloudc2.service
```

Paste in the following text. **NOTE:** Replace parameters as necessary for your instance

```
[Unit]
Description=Hak5 Cloud C2
After=cloudc2.service
[Service]
Type=idle
ExecStart=/usr/local/bin/c2-3.5.2_amd64_linux -hostname DOMAIN -https -db /var/cloudc2/c2.db
[Install]
WantedBy=multi-user.target
```

Finally, reload, enable on boot, start and inspect the newly created Cloud C2 service

```
sudo systemctl daemon-reload
sudo systemctl enable cloudc2.service
sudo systemctl start cloudc2.service
```

## Adding Devices

* WiFi Pineapple – put `device.config` in `/etc/`
* LAN Turtle – put `device.config` in `/etc/`
* Packet Squirrel – put `device.config` in `/etc/`
* Signal Owl – put `device.config` in `/etc/` and use `C2CONNECT` in your payload
* Shark Jack – put `device.config` in `/etc/` and use `C2CONNECT` in your payload
* Screen Crab – put `device.config` on the root of the SD card
* Key Croc – put `device.config` on the root of the KeyCroc disk from arming mode

Generally, once the device is online it’ll connect back to Cloud C² and you’ll be able to interact with it from the dashboard. The exception to this is the Shark Jack and Signal Owl, which require the command `C2CONNECT` in the payload to initialize the connection.

Likewise, run the `C2DISCONNECT` command to cut the connection. This is by design so that you aren’t inadvertently connecting to your Cloud C² instance from every Shark Jack payload you run, as an example.

Many devices support the `C2NOTIFY` and `C2EXFIL` commands to send notifications and exfiltrate loot. The `C2EXFIL` command must be run for each file uploaded to the Cloud C² server.

When exfiltrating text files, you’ll want to add the `STRING` option in order to make it viewable from the dashboard. For example, `C2EXFIL STRING /root/loot/file.txt MyPayloadName`
