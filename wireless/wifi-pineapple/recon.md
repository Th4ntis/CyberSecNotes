# Recon

To start Recon we select the binocular icon on the left.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133747.png" alt=""><figcaption></figcaption></figure>

We can choose which frequency we wanna scan on, how long we want to scan, and other settings, like where to save handshakes, what we want and don't want to see, etc.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133750.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250909133754.png" alt=""><figcaption></figcaption></figure>

To start scanning, just enable the button. Once we start scanning, we will see a list of all AP's and devices around. We can also sort or search it by our filters to help us find our target(s).&#x20;

<figure><img src="../../.gitbook/assets/Pasted image 20250909133800.png" alt=""><figcaption></figcaption></figure>

Once we have our target(s) in sight, we can select it for a list of options we can do.&#x20;

<figure><img src="../../.gitbook/assets/Pasted image 20250909133808.png" alt=""><figcaption></figcaption></figure>

* Adding SSID to the PineAP Pool will have the Pineapple Broadcast as that network. This is best used on Open WiFi.
* Add SSID to Filter - Allows/Denies the selected SSID to associate with the pineapple.
* Add All Clients to Filter - Allows/Denies the selected clients to connect to the pineapple.
* Deauthentice All Clients - Will attempt to kick off all clients on that SSID to either reconnect, or force them to connect to another AP they have connected to before.
* Capture WPA Handshakes - Attempt to get a handshake.
* Clone WPA/2 AP - Attemps to X

When we stop scanning, the scans are saved in the Previous Scans section to download a .json file and view.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133815.png" alt=""><figcaption></figcaption></figure>

## Handshakes

When we choose to Capture a WPA Handshake, it will keep waiting for a handshake(wait for someoen to connect to the AP), OR we can deauth clients that are connected to the AP and force them to re-connect and capture a handshake.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133818.png" alt=""><figcaption></figcaption></figure>

When attempting to deauth an SSID/AP with Management Frame Protection (MFP) optional/enabled. It will bring up a pop-up explaining it.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133822.png" alt=""><figcaption></figcaption></figure>

When a handshake is captured, we will see a notification in the top right, as well as the Wireless Landscape Dashboard will show us how many handshakes we have captured.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133826.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250909133829.png" alt=""><figcaption></figcaption></figure>

Now we can verify it by either opening the web terminal or SSH, and looking at the `/root/handshakes` folder.

```bash
ls /root/handshakes
```

<figure><img src="../../.gitbook/assets/Pasted image 20250909133834.png" alt=""><figcaption></figcaption></figure>

We will need to use either [scp](https://www.geeksforgeeks.org/scp-command-in-linux-with-examples/) or [WinSCP](https://winscp.net/eng/index.php) to copy the files off of the Pineapple for cracking.
