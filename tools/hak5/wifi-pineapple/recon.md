# Recon

## Recon

Recon is the Pineapple's wireless landscape scanner - it puts a radio into monitor mode, channel-hops, and builds a live list of the access points and clients around you. More info on the [docs](https://docs.hak5.org/wifi-pineapple/ui-overview/recon-1).

To start Recon we select the binocular icon on the left. !\[\[Pasted image 20250909133747.png]]

We can choose which frequency we wanna scan on, how long we want to scan, and other settings, like where to save handshakes, what we want and don't want to see, etc. !\[\[Pasted image 20250909133750.png]] !\[\[Pasted image 20250909133754.png]]

> **Bands & channels:** the built-in radio covers **2.4 GHz** (14 channels; 1/6/11/14 are the non-overlapping ones). With the **MK7AC** adapter you also get **5 GHz** (U-NII bands, 45 channels at 20/40/80/160 MHz in the US). Regulatory domain matters: North America uses channels 1–11, most of the world 1–13, Japan all 14.
>
> The **gear/settings menu** lets you choose the scan location, which columns to show, expand all client lists, and highlight active devices. There's also a _Tagged Parameters_ view and a _Security Information_ panel.

To start scanning, just enable the button. Once we start scanning, we will see a list of all APs and devices around. We can also sort or search it by our filters to help us find our target(s). !\[\[Pasted image 20250909133800.png]]

Once we have our target(s) in sight, we can select it for a list of options we can do. !\[\[Pasted image 20250909133808.png]]

* **Add SSID to the PineAP Pool** - has the Pineapple broadcast as that network. This is best used on Open WiFi.
* **Add SSID to Filter** - Allows/Denies the selected SSID to associate with the Pineapple.
* **Add All Clients to Filter** - Allows/Denies the selected clients to connect to the Pineapple.
* **Deauthenticate All Clients** - attempts to kick all clients off that SSID, forcing them to reconnect (which can yield a handshake) or to roam to another AP they've connected to before.
* **Capture WPA Handshakes** - attempt to capture a 4-way handshake.
* **Clone WPA/2 AP** - spins up an **Evil Twin**: it takes the selected AP's SSID, BSSID, and channel and stands up a matching rogue AP (via Evil WPA/Twin) so clients associate with the Pineapple instead of the real network. If the PSK is unknown, it can still collect partial handshakes for offline cracking.

When we stop scanning, the scans are saved in the **Previous Scans** section to download a `.json` file and view. !\[\[Pasted image 20250909133815.png]]

## Handshakes

When we choose to Capture a WPA Handshake, it will keep waiting for a handshake (wait for someone to connect to the AP), OR we can deauth clients that are connected to the AP and force them to re-connect and capture a handshake. !\[\[Pasted image 20250909133818.png]]

> **Handshakes come from two sources:** _Recon Capture_ (direct capture parks the radio on the target's channel) and _Evil WPA/2 Twin_. Automatic capture is toggled in the Recon panel. Each handshake is saved in both **PCAP** and **Hashcat 22000** formats. The default save location is `/root/handshakes` (changeable via the Settings icon).

When attempting to deauth an SSID/AP with Management Frame Protection (MFP) optional/enabled, it will bring up a pop-up explaining it. !\[\[Pasted image 20250909133822.png]]

> **Why MFP blocks deauth:** deauthentication frames are management frames. If the target uses **MFP (802.11w)**, **WPA3**, or sits on **DFS / UNII-2 / UNII-2e** channels, the Pineapple can't deauth it. If no clients are visible on the target, you'll get a warning and the option to send a **broadcast disassociation** instead.

When a handshake is captured, we will see a notification in the top right, and the Wireless Landscape Dashboard will show us how many handshakes we have captured. !\[\[Pasted image 20250909133826.png]] !\[\[Pasted image 20250909133829.png]]

Now we can verify it by either opening the web terminal or SSH, and looking at the `/root/handshakes` folder.

```bash
ls /root/handshakes
```

!\[\[Pasted image 20250909133834.png]]

We will need to use either [scp](https://www.geeksforgeeks.org/scp-command-in-linux-with-examples/) or [WinSCP](https://winscp.net/eng/index.php) to copy the files off of the Pineapple for cracking.

```bash
scp root@172.16.42.1:/root/handshakes/* .
```

> **Cracking:** the `.22000` files drop straight into **hashcat** (`hashcat -m 22000 handshake.22000 wordlist.txt`); the `.pcap` files can be converted or opened in Wireshark/`aircrack-ng` as needed.

## Related notes

* \[\[PineAP]] - Evil WPA / Evil Twin that Clone uses
* \[\[Basics]] - choosing the recon interface (MK7AC for 5 GHz)
