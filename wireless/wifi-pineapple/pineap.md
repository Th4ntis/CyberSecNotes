# PineAP

PineAP is PineAP is the center of the WiFi Pineapple's rogue access points, client management and filtering. - More info on PineAP [here](https://docs.hak5.org/wifi-pineapple/ui-overview/pineap#pineap-settings).

Our FIlter list here is VERY important as if this is not configured right, we can end up with targets that we are not authorized to be testing. More info on filtering is [here on their docs](https://docs.hak5.org/wifi-pineapple/ui-overview/pineap#filtering). I choose Allow for both filters by default as to not allow any unwanted/unallowed connections.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133645.png" alt=""><figcaption></figcaption></figure>

### Client Filter

This chooses what devices may or may not connect.

* Allow - Only the allowed listed devices can connect.
* Deny - All devices can connect except the listed devices.

### SSID Filter

This specifies the spoofed networks for which the WiFi Pineapple will allow associations.

## Open AP

The WiFi Pineapple can advertise a single Open SSID, or respond for any requested SSID that matches the filter rules.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133651.png" alt=""><figcaption></figcaption></figure>

Multiple Open Access Points. When "Impersonate All Networks" is enabled, the WiFi Pineapple will answer for all SSIDs which are permitted by the filter configuration. Filters can be used to tune the responses for your engagement, by either allowing all SSIDs in the filter list, or denying all SSIDs not in the filter list.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133655.png" alt=""><figcaption></figcaption></figure>

## Evil WPA

The Evil WPA access point is used to impersonate a WPA (or WPA2) PSK network. It can also be used to collect partial handshakes for use with external cracking tools when the PSK is not known.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133659.png" alt=""><figcaption></figcaption></figure>

Here we want to name our Evil WPA SSID after our target(s), and spoof the target(s) MAC address as well. Be sure to add the target(s) SSID to the SSID Filter.
