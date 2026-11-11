# Evil Portal

## Evil Portal

The [WiFi Pineapple](https://shop.hak5.org/collections/wifi-pentesting/products/wifi-pineapple) is developed by [Hak5](https://hak5.org/). From their website: _"Automate WiFi auditing with all new campaigns and get actionable results from vulnerability assessment reports. Command the airspace with a new interactive recon dashboard, and stay on-target and in-scope with the leading rogue access point suite for advanced man-in-the-middle attacks._

_Next-gen network processors combine with multiple role-based radios and the Hak5 patented PineAP suite to deliver impressive results. Hardened and stress tested for the most challenging environments._

_The new WiFi Pineapple Mark VII features incredible performance from a simple web interface with an expansive ecosystem of apps, automated pentest campaigns, and Cloud C2 for remote access from anywhere."_

> **What an Evil Portal is:** a **captive portal** (the "sign-in" page you see on public WiFi) served by the Pineapple's Open AP. When a client connects, all their web traffic is redirected to a page you control - commonly a cloned login (Google, hotel WiFi, corporate SSO, etc.) - so you can demonstrate credential harvesting. It's the Pineapple pairing its **Open AP** (\[\[PineAP]]) with a web server + DNS redirect. The **Evil Portal module** provides the UI for all of this.

## Setting up the portal

I was unable to clone the repository directly to my Pineapple, so I cloned it to my machine and copied it to the Pineapple under `/root/portals/`. I took some of [Kleo's Evil Portals](https://github.com/kleo/evilportals) as I'm not skilled enough to make my own.

```bash
git clone https://github.com/Th4ntis/Evil-Portals.git
scp -r Evil-Portals/* root@172.16.42.1:/root/portals/
```

> **Portal layout:** each portal lives in its own folder under `/root/portals/`, typically containing an `index.php`/`index.html` (the page shown), a `MyPortal.php` helper, and a `*.ep` marker file the module uses to list it. Browsing the Kleo repo gives you ready-made templates to drop in.

Download the **Evil Portal** module from the Pineapple Modules (see \[\[Modules]]). !\[\[Pasted image 20250909133457.png]]

Once installed, open the module and **install dependencies**. Now we can preview the portals by activating the portal. !\[\[Pasted image 20250909133502.png]]

Once activated, start the web server, then we can preview it. !\[\[Pasted image 20250909133505.png]]

Now, we go to our **Open AP**, set the desired WiFi name, BSSID, and channel. !\[\[Pasted image 20250909133511.png]]

Start the server with the Evil Portal. Now when a client is connected, on the home page we will see their MAC address and IP address. !\[\[Pasted image 20250909133516.png]]

Take the IP address and add it into the Evil Portal's **allowed clients**. !\[\[Pasted image 20250909133521.png]]

> **Why "allowed clients"?** The portal holds unauthorized clients on the login page. Once a client "authenticates" (or you manually allow their IP), they're added to the allow list and let through to the internet - mimicking how a real captive portal grants access after sign-in.

Now when the client is connected they are sent to an authorization login page - Google in this case. !\[\[Pasted image 20250909133526.png]]

If they enter their credentials, their page shows they aren't authorized. !\[\[Pasted image 20250909133531.png]]

We also get a notification on our Pineapple page. !\[\[Pasted image 20250909133536.png]]

We can view the logs from the Evil Portal page to see the email, password, hostname, MAC, and IP that were entered. !\[\[Pasted image 20250909133541.png]] !\[\[Pasted image 20250909133545.png]]

> **Logs & loot:** captured credentials are written to the module's log (viewable in the Evil Portal UI, and on disk under the portal/module directory). Pull them off with `scp`/WinSCP like any other loot.

> ⚠️ **Authorization & ethics:** capturing credentials is only legal against assets you're explicitly authorized to test. Keep your \[\[PineAP]] filters scoped to your engagement so you don't trap bystanders, and handle any captured credentials as sensitive data.

## Related notes

* \[\[Modules]] - installing the Evil Portal module
* \[\[PineAP]] - the Open AP the portal rides on
* \[\[Basics]] - getting internet to the Pineapple so clients stay connected
