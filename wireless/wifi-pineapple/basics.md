# Basics

## About

The [WiFi Pineapple](https://shop.hak5.org/products/wifi-pineapple) from [Hak5](https://hak5.org/) is a wireless auditing platform that allows network security administrators to conduct wireless penetration tests. It has multiple features including the ability to create rogue access points, man-in-the-middle attacks, perform passive surveillance, WPA and WPA Enterprise attacks, and more. More info can be found on [their docs page](https://docs.hak5.org/wifi-pineapple).

By default it uses 2.4GHz frequency but you can get their `MK7AC WiFi Adapter` that will add 2.5GHz and 5GHz frequencies. You are able to use your own adapters but they not work well with the pineapple, so your milage may vary depending on device.

## Setup

### Windows

Now if we want to share our internet connection from our PC to the Pineapple, we need to also select the interface that our internet comes in on(Wi-Fi in my case) and share it to the Pineapple.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133245.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250909133249.png" alt=""><figcaption></figcaption></figure>

Now we need to set the IP for it:

```
IP: 172.16.42.42
Subnet: 255.255.0.0
Gateway: blank
DNS: Whatever you want, I usually use Cloudflare(1.1.1.1) or Quad9(9.9.9.9)
```

<figure><img src="../../.gitbook/assets/Pasted image 20250909133256.png" alt=""><figcaption></figcaption></figure>

### Linux

To share our internet from our host machine to the Pineapple, we can run a python script I made. The github page can found [here](https://github.com/Th4ntis/Debian-Internet-Sharing).

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

This will ask for your internet-facing device, then ask for the Pineapples interface. We can find both of those with

```bash
ip a
```

<figure><img src="../../.gitbook/assets/Pasted image 20250909133314.png" alt=""><figcaption></figcaption></figure>

then run the script

<figure><img src="../../.gitbook/assets/Pasted image 20250909133318.png" alt=""><figcaption></figcaption></figure>

## WebUI

Now we can go to the Web Interface in our browser by going to [http://172.16.42.1:1471/](http://172.16.42.1:1471/)

<figure><img src="../../.gitbook/assets/Pasted image 20250909133327.png" alt=""><figcaption></figcaption></figure>

This option is up to you on which you prefer - I went with Radios disabled

<figure><img src="../../.gitbook/assets/Pasted image 20250909133338.png" alt=""><figcaption></figcaption></figure>

After a few more prompts we will be asked for put our root password and timezone.&#x20;

<figure><img src="../../.gitbook/assets/Pasted image 20250909133343.png" alt=""><figcaption></figcaption></figure>

Now we set our AP's. The Management AP we will connect to to access the dashboard and tools and etc. The Open AP is the one your target(s) will be connecting to. I usually hide the management AP but it's up to you on what you would like to do.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133349.png" alt=""><figcaption></figcaption></figure>

Now we get to an important step, the Client Filter and SSID Filter. by default I put mine to allow that way not just anyone can connect and use it, we want our specified target(s) to connect. If we have their MAC address or SSID, we can add them now, or move onto the next step.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133357.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250909133401.png" alt=""><figcaption></figcaption></figure>

Now choose your theme and accept their EULA. After a min or so we are redirected to the login page and after we login, we have the dashboard!

<figure><img src="../../.gitbook/assets/Pasted image 20250909133407.png" alt=""><figcaption></figcaption></figure>

If we have the MK7AC Adapter plugged in, we get a prompt for it, but we can close that for now.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133411.png" alt=""><figcaption></figcaption></figure>

### Internet Setup

So we have some options for setting up the internet to the Pineapple. This step is important because it's what will keep traffic flowing throw the target(s) to the internet for them to stay connected to us.

* Wireless Client Mode - This will require us to have an SSID and Password for the Pineapple to connect to.
* ICS(Internet Connection Sharing) - This will allow us to share the internet connection from our machine the Pineapple is plugged into.
* USB Ethernet Adapter - If we have a USB to Ethernet dongle plugged into the Pineapple we can use this method for a hardwired connection.

When you know which one you want, select the `Network Setting` button. I typically prefer to go with ICS as we set that up before this.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133420.png" alt=""><figcaption></figcaption></figure>

While here, if we have the MK7AC module plugged in, we can change our `Recon Wireless Interface`to that and select save.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133424.png" alt=""><figcaption></figcaption></figure>

Whichever option you choose, you can verify internet connection by clicking the terminal icon in the top right and ping something to test.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133428.png" alt=""><figcaption></figcaption></figure>
