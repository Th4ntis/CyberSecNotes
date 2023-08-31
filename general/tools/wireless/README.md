# Wireless

Wireless is everywhere, home, work, school, you name it, which is convenient for a lot of people as they have tablets, phones, laptops, etc that don't always have an ethernet to be hardwired in but if not properly secured it can leave the network open to attacks for an attacker to get into the network and perform various attacks, such as gaining access to a machine and harvest credentials, or man-in-the-middle attacks where they intercept network traffic for a multitude of reasons.&#x20;

For information regarding wireless networking refer to [this](../../networking/wireless/). Popular, and helpful wireless auditing tools:

* [Aircrack](aircrack-ng.md)
* [Kismet](kismet.md)
* [Bettercap](bettercap.md)

## Defense

A good way to defend your wireless network is to have a strong wireless password, pretty simple. Don't use your phone number, a family members name, or anything that one can guess simply by talking to you to find basic information. Especially since you don't need to type it in that often. This makes it more difficult for an attacker to crack your wireless password if they obtain a handshake or PMKid for offline cracking.

Keep an eye out when connecting to a network you have previously connected to that is saved in your device. If you are directed to a web page that asks you to verify your network password, do not enter your password as that is likely an '[Evil Twin](https://www.varonis.com/blog/evil-twin-attack)' attack, where someone is pretending to be your network, forcing you to connect to their network, and when you enter the password, it's given to the attacker in plain text for them to then connect to your network.

If possible, segment your network. If you have a second access point to use, you can set that up for guests for them to use, but that can be segmented from the rest of your network so they can't access your devices easily. Each network can have a separate name and password.
