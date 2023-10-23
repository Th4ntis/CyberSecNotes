# Wardriving/WiFi Sniffing

## About

War driving, also known as "WiFi sniffing" is the process of locating WiFi networks, and potentially sniffing their traffic. War driving involves searching for wireless networks with vulnerabilities while moving around an area in various methods such as driving, walking, or biking. They use hardware and software to discover unsecured WiFi networks then can gain unauthorized access to the network by cracking WiFi passwords. Then records vulnerable network locations on digital maps, known as access point mapping, and may share that information with third-party applications or websites.&#x20;

As mentioned before this is able to detect unsecured WiFi traffic. So when you're connected to an open public WiFi, sniffing is able to capture and log the traffic between your machine and the access point, and potentially capture unsecured credentials when logging into an insecure website, or gather encrypted traffic to attempt to decrypt later.

In some cases, a method of war driving is also capturing encrypted WiFi passwords in the form of a Handshake or a PMKid, using methods and tools like [aircrack](../../tools/wireless/aircrack-ng.md) or [hcxdumpttool](../../tools/wireless/hcxdumptool.md), to then crack later and connect to later.

## Methods

There's multiple ways of war driving, using your laptop a [Raspberry Pi](https://www.raspberrypi.com/) with appropriate devices such as [GPS adapters](https://www.amazon.com/gp/product/B01EROIUEW/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8\&psc=1), [antennas](https://www.amazon.com/gp/product/B08SJBV1N3/ref=ppx\_yo\_dt\_b\_search\_asin\_title?ie=UTF8\&psc=1), or even your phone with the [WiGLE WiFi app](https://play.google.com/store/apps/details?id=net.wigle.wigleandroid\&utm\_source=global\_co\&utm\_medium=prtnr\&utm\_content=Mar2515\&utm\_campaign=PartBadge\&pcampaignid=MKT-AC-global-none-all-co-pr-py-PartBadges-Oct1515-1). Popular softwares include [Wireshark](../wireshark.md), [Kismet](../../tools/wireless/kismet.md), or use specified devices such as the [WiFi Coconut](https://hakshop.com/products/wifi-coconut) from [Hak5](https://hak5.org/pages/about).

### Is this legal?

This is a bit of a grey area in some cases/areas and depending what you doing, weather you're just scanning networks and nothing more, or attempting to gather WiFi hashes. Typically this is not as it's just collecting basic public information, such as the WiFi name(BSSID), the security(WPA, WPA2, etc), and location(using GPS). This isn't inherently malicious or nefarious but it _could_ be used that way by those with malicious intent.
