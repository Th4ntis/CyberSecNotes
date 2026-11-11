# PineAP

## PineAP

PineAP is the center of the WiFi Pineapple's rogue access points, client management and filtering. More info on PineAP [here](https://docs.hak5.org/wifi-pineapple/ui-overview/pineap#pineap-settings).

Our filter list here is **VERY** important - if this is not configured right, we can end up with targets that we are not authorized to be testing. More info on filtering is [here on their docs](https://docs.hak5.org/wifi-pineapple/ui-overview/pineap#filtering). I choose **Allow** for both filters by default so as not to allow any unwanted/unallowed connections. !\[\[Pasted image 20250909133645.png]]

### PineAP modes

The suite can run in three overall modes:

* **Passive** - collects nearby APs and accepts connections to your configured Open/WPA/Enterprise SSIDs, but does **not** advertise other networks.
* **Active** - advertises the Impersonated AP (SSID) Pool and answers all permitted probe requests.
* **Advanced** - turn each feature (impersonation, open AP, evil WPA, etc.) on or off individually.

### Client Filter

This chooses what devices may or may not connect.

* **Allow** - Only the allowed listed devices can connect.
* **Deny** - All devices can connect except the listed devices.

### SSID Filter

This specifies the spoofed networks for which the WiFi Pineapple will allow associations.

* **Allow** - only listed SSIDs are answered.
* **Deny** - everything except listed SSIDs is answered.

> ⚠️ You must **Allow** the Open or Evil WPA SSID (and the target clients) or they won't be able to connect. The common engagement pattern is: **SSID Filter = Allow** with your target SSIDs listed, and **Client Filter = Deny** with an empty list (any client can connect, but only to your in-scope SSIDs). Filter changes take effect immediately.

## Open AP

The WiFi Pineapple can advertise a single Open SSID, or respond for any requested SSID that matches the filter rules. !\[\[Pasted image 20250909133651.png]]

**Multiple Open Access Points.** When "Impersonate All Networks" is enabled, the WiFi Pineapple will answer for all SSIDs which are permitted by the filter configuration. Filters can be used to tune the responses for your engagement, by either allowing all SSIDs in the filter list, or denying all SSIDs not in the filter list. !\[\[Pasted image 20250909133655.png]]

> The Open SSID can be **visible or hidden**, but hidden SSIDs are still probed for by clients that have seen them before, so hiding isn't a guarantee of stealth.

### SSID / Impersonation Pool

* **Capture SSIDs to Pool** adds SSIDs seen in probe requests and in Recon.
* **Broadcast SSID Pool** actively advertises them (Active mode).
* Advertise using one BSSID, or a pseudo-random BSSID per SSID (note: many clients reject random-BSSID networks).

## Evil WPA

The Evil WPA access point is used to impersonate a WPA (or WPA2) PSK network. It can also be used to collect partial handshakes (PMKID) for use with external cracking tools when the PSK is not known. !\[\[Pasted image 20250909133659.png]]

Here we want to name our Evil WPA SSID after our target(s), and spoof the target(s) MAC address (BSSID) as well. Be sure to add the target(s) SSID to the SSID Filter. Captured handshakes show up in the **Handshakes** area (see \[\[Recon]]).

## Evil Enterprise (WPA-EAP)

The Pineapple can also impersonate a **WPA-Enterprise (802.1X/EAP)** network to capture credentials:

* Certificate generation can take **up to 5 minutes** the first time.
* Auth methods: **Any**, **MSCHAPv2** (captures the challenge/response **hash** for offline cracking), or **GTC** (captures the **plaintext** username and password).

## Event logs & clients

* PineAP logs **probes, associations, and disassociations**; connect/disconnect notifications are optional.
* The **Clients** page shows **Connected** clients (which you can **kick**) and **Previous** clients.

## Related notes

* \[\[Recon]] - finding targets and capturing handshakes
* \[\[Basics]] - initial filter setup during the wizard
* \[\[Evil Portal]] - pairing the Open AP with a captive portal
