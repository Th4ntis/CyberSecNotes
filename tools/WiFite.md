# About
[Wifite](https://github.com/kimocoder/wifite2) is a tool written in python used for pentesting wireless networks. It's an automated tool that utilizes [aircrack-ng](https://cybersec.th4ntis.com/tools/wireless/aircrack-ng), and other tools such as [hcxdumptool](https://cybersec.th4ntis.com/tools/wireless/hcxdumptool), tshark, bully, reaver, and more to obtain WiFi handshakes, PMKID attacks. That also can perform WPS and WEP attacks.
# Installing
Install prerequisites
```
git clone https://github.com/kimocoder/wifite2.git
cd wifite2 && pip3 install -r requirements.txt
```
## Running and installing to system
To run wifite without installing, run it from the repository
```
sudo ./wifite.py
```

To install it to the system
```
sudo python3 setup.py install
```
# Usage
To show various types of attacks and arguments we can use
```
sudo wifite -h
```

We can specify a wireless interface with
```
sudo wifite -i (interface)
```

OR if we only have one WiFi interface on that is capable of monitor mode, we can just run it as is.
## WPA
We can do a WPA attack on a target network with
```
sudo wifite --wpa
```

This will enable monitor mode on the wireless interface and begin scanning for networks.

I will target Pixel7, number 2
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FVpx0yYgNCGKxc5svPVFj%252Fimage.png%3Falt%3Dmedia%26token%3Dd8255d21-3b91-47bf-9dfe-063d15357ba5&width=768&dpr=4&quality=100&sign=f8304400&sv=2)

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FY9OfJ61TMUFzUpzByORX%252Fimage.png%3Falt%3Dmedia%26token%3D46257848-c36b-4927-a4ee-e059d14cbfc4&width=768&dpr=4&quality=100&sign=308959b4&sv=2)

This starts with a PMKID attack, then moves onto a WPA Handshake attack if a PMKID is unable to be obtained.
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FlBsS67rJ2zo9wc5Q774U%252Fimage.png%3Falt%3Dmedia%26token%3D522890d6-d2fb-499f-afdd-8fd604068c39&width=768&dpr=4&quality=100&sign=7049aa84&sv=2)

*Note, we can skip the PMKID attack by adding the argument `--no-pmkid`
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FKbC6Q4rbiO4oem4EcuS2%252Fimage.png%3Falt%3Dmedia%26token%3Ddc5e1615-5998-4465-bd13-35a7547bb491&width=768&dpr=4&quality=100&sign=c888c424&sv=2)

When obtaining a WPA handshake attack, this will attempt to de-authenticate clients from the network until we have obtained the handshake.

When the handshake is captured we see where it was saved to with the name of it. It will attempt to crack it automatically with `aircrack-ng` using their default worldlist `wordlist-probably.txt`
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FHZeAT1pDg5ipqgFgc1vM%252Fimage.png%3Falt%3Dmedia%26token%3Dd3dde13c-ad11-462a-800e-1b952e16e462&width=768&dpr=4&quality=100&sign=19ec0ecc&sv=2)

If you would like to use your own dictionary, such as `rockyou.txt` we can use the `--dict` argument.
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FEoeyJzWJVAeOoSqpn1yY%252Fimage.png%3Falt%3Dmedia%26token%3D64aa93aa-204c-4f41-ace6-37bf31b977e3&width=768&dpr=4&quality=100&sign=92a126a0&sv=2)