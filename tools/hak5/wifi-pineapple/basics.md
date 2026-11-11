# Basics

## Basics

The [WiFi Pineapple](https://shop.hak5.org/products/wifi-pineapple) from [Hak5](https://hak5.org/) is a wireless auditing platform that allows network security administrators to conduct wireless penetration tests. It has multiple features including the ability to create rogue access points, man-in-the-middle attacks, perform passive surveillance, WPA and WPA Enterprise attacks, and more. More info can be found on [their docs page](https://docs.hak5.org/wifi-pineapple).

By default it uses the 2.4 GHz frequency, but you can get their `MK7AC WiFi Adapter` that will add **5 GHz** support. You are able to use your own adapters but they may not work well with the pineapple, so your mileage may vary depending on the device.

> **Which model is which:** the standard **Mark VII (MK7)** is **2.4 GHz only** (based on MediaTek **MT7601U / MT7610U** chipsets). Adding the **MK7AC** USB adapter gives you dual-band **2.4 / 5 GHz** recon. The **Mark VII Enterprise** edition ships with dual-band radios built in.

### Hardware & interfaces at a glance

| Item              | Detail                                                                                                                                                                 |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Bands             | 2.4 GHz built-in; 5 GHz via MK7AC adapter (or Enterprise).                                                                                                             |
| Recon radio       | `wlan1` (built-in 2.4 GHz) by default; `wlan3` appears when a compatible USB adapter is connected (2.4/5 GHz).                                                         |
| Client-mode radio | `wlan2` - Hak5 recommends dedicating this interface to Wireless Client Mode.                                                                                           |
| Management IP     | `172.16.42.1`                                                                                                                                                          |
| WebUI             | `http://172.16.42.1:1471` - **the `:1471` is required**; the default port returns a blank page.                                                                        |
| Power             | Use a **2 A or higher** supply. USB-C PD adapters sometimes fail to deliver 5 V - a plain USB-A 2 A adapter is a reliable fallback; battery banks need 2 A continuous. |
| Antennas          | **Connect antennas before powering on** - transmitting without them can damage the radios.                                                                             |
| LEDs              | Red / Green / Blue, each independently set to _Default Off_, _Default On_, _Heartbeat_ (pulses faster under CPU load), or _Network device_ (blinks on packets).        |
| Reset             | Hold the reset button **10+ seconds** after boot to reset the password (firmware 1.1.0+).                                                                              |

## Setup

### Windows

Now if we want to share our internet connection from our PC to the Pineapple, we need to also select the interface that our internet comes in on (Wi-Fi in my case) and share it to the Pineapple. !\[\[Pasted image 20250909133245.png]] !\[\[Pasted image 20250909133249.png]]

Now we need to set the IP for it:

```
IP: 172.16.42.42
Subnet: 255.255.0.0
Gateway: blank
DNS: Whatever you want, I usually use Cloudflare(1.1.1.1) or Quad9(9.9.9.9)
```

!\[\[Pasted image 20250909133256.png]]

> This gives your PC a static address (`172.16.42.42`) on the same subnet as the Pineapple's management IP (`172.16.42.1`), so you can reach the WebUI and share internet to it.

### Linux

To share our internet from our host machine to the Pineapple, we can run a python script I made. The github page can be found [here](https://github.com/Th4ntis/Debian-Internet-Sharing).

The script is

```python
#!/usr/bin/env python3
import subprocess

def run_command(command):
    """Run a shell command."""
    try:
        subprocess.check_call(command, shell=True)
    except subprocess.CalledProcessError as e:
        print(f"An error occurred: {e}")

def setup_internet_sharing(internet_interface, device_interface):
    """Set up internet sharing from the internet interface to another USB/RNDIS Device."""
    # Enable IP forwarding
    run_command("echo 1 > /proc/sys/net/ipv4/ip_forward")

    # Configure NAT over iptables
    run_command(f"iptables -t nat -A POSTROUTING -o {internet_interface} -j MASQUERADE")
    run_command(f"iptables -A FORWARD -i {internet_interface} -o {device_interface} -m state --state RELATED,ESTABLISHED -j ACCEPT")
    run_command(f"iptables -A FORWARD -i {device_interface} -o {internet_interface} -j ACCEPT")

    # Assign an IP address to the Devices interface if needed
    run_command(f"ifconfig {device_interface} 172.16.42.1 netmask 255.255.0.0")

    print("Internet sharing setup complete.")

if __name__ == "__main__":
    internet_interface = input("Enter the name of your internet-facing interface (e.g., eth0, wlan0): ")
    device_interface = input("Enter the name of your USB/RNDIS devices interface (e.g., eth1): ")
    setup_internet_sharing(internet_interface, device_interface)
```

This will ask for your internet-facing device, then ask for the Pineapple's interface. We can find both of those with

```bash
ip a
```

!\[\[Pasted image 20250909133314.png]]

then run the script !\[\[Pasted image 20250909133318.png]]

> **What the script does:** enables IPv4 forwarding, sets up NAT (`MASQUERADE`) out your internet interface, allows forwarding both directions between the two interfaces, and assigns `172.16.42.1` to the Pineapple-facing interface. Run it as **root** (`sudo`). The NAT rules aren't persistent - they reset on reboot, so re-run it each session (or save your iptables rules if you want them to stick).

## WebUI

Now we can go to the Web Interface in our browser by going to [http://172.16.42.1:1471/](http://172.16.42.1:1471/) !\[\[Pasted image 20250909133327.png]]

> First boot runs a setup wizard. If the Pineapple is still on the slim _stager_ firmware, you'll be prompted to flash the full firmware first (either over-the-air by joining a WPA/WPA2 network, or by uploading a firmware image downloaded from [downloads.hak5.org](https://downloads.hak5.org/pineapple) - verify the SHA256). Flashing takes \~10–15 minutes.

This option is up to you on which you prefer - I went with Radios disabled !\[\[Pasted image 20250909133338.png]]

After a few more prompts we will be asked to put in our root password and timezone. !\[\[Pasted image 20250909133343.png]]

Now we set our AP's. The Management AP we will connect to to access the dashboard and tools, etc. The Open AP is the one your target(s) will be connecting to. I usually hide the management AP but it's up to you on what you would like to do. !\[\[Pasted image 20250909133349.png]]

Now we get to an important step, the Client Filter and SSID Filter. By default I put mine to allow so that not just anyone can connect and use it - we want our specified target(s) to connect. If we have their MAC address or SSID, we can add them now, or move onto the next step. !\[\[Pasted image 20250909133357.png]] !\[\[Pasted image 20250909133401.png]]

> ⚠️ **Scope control lives here.** Allow-mode filters with your authorized targets listed are what keep you from capturing out-of-scope devices. More on this in \[\[PineAP]].

Now choose your theme and accept their EULA. After a min or so we are redirected to the login page and after we login, we have the dashboard! !\[\[Pasted image 20250909133407.png]]

If we have the MK7AC Adapter plugged in, we get a prompt for it, but we can close that for now. !\[\[Pasted image 20250909133411.png]]

### Internet Setup

So we have some options for setting up the internet to the Pineapple. This step is important because it's what will keep traffic flowing through the target(s) to the internet for them to stay connected to us.

* **Wireless Client Mode** - This will require us to have an SSID and Password for the Pineapple to connect to (uses `wlan2`). It reconnects on boot.
* **ICS (Internet Connection Sharing)** - This will allow us to share the internet connection from our machine the Pineapple is plugged into (the Windows/Linux steps above).
* **USB Ethernet Adapter** - If we have a USB to Ethernet dongle plugged into the Pineapple we can use this method for a hardwired connection (DHCP by default, or set a static IP).

When you know which one you want, select the `Network Settings` button. I typically prefer to go with ICS as we set that up before this. !\[\[Pasted image 20250909133420.png]]

While here, if we have the MK7AC module plugged in, we can change our `Recon Wireless Interface` to that and select save. !\[\[Pasted image 20250909133424.png]]

Whichever option you choose, you can verify internet connection by clicking the terminal icon in the top right (or pressing the backtick `` ` `` key) and ping something to test. !\[\[Pasted image 20250909133428.png]]

## Accessing the device

* **WebUI:** `http://172.16.42.1:1471` (login `root` + the password you set).
* **Web Terminal:** terminal icon, top-right, or the backtick (`` ` ``) key.
* **SSH:** `ssh root@172.16.42.1`.

## Related notes

* \[\[PineAP]] - rogue AP suite and filtering
* \[\[Recon]] - scanning and handshake capture
* \[\[Modules]] - extending the Pineapple
* \[\[Evil Portal]] - captive-portal credential harvesting
