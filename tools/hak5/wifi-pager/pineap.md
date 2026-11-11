# PineAP

## Pager PineAP

The WiFi Pineapple PineAP functionality controls network impersonation, client capture, connection filters, and the EvilWPA access point.

Understanding and configuring PineAP is crucial to properly scoping an engagement and limiting the impacted devices, and the PineAP display panel aims to make this as simple and reliable as possible!

> ⚠️ **Filters first.** A misconfigured filter is how you accidentally capture devices you aren't authorized to test. See **PineAP Filters** below and keep the allow/deny logic tight before enabling any AP.

### Links

* [Docs](https://docs.hak5.org/wifi-pineapple-pager/pineap/)

### Where to find each setting on-device

| Feature             | Path                                    |
| ------------------- | --------------------------------------- |
| Open AP             | `PineAP → Open AP`                      |
| Mimic Open Networks | `PineAP → PineAP → Mimic Open Networks` |
| Collect Probes      | `PineAP → Collect Probes`               |
| Advertise Network   | `PineAP → Advertise Network`            |
| SSID Pool           | `PineAP → SSID Pool`                    |
| Filters             | `PineAP → Filters`                      |
| Evil WPA            | `PineAP → Evil WPA`                     |

## PineAP Config

The PineAP Open Access Point functions as a trap for clients configured for connections to unencrypted access points.

The PineAP Open Access Point can capture a broad range of clients by mimicking multiple network names and automatically responding to any network requested. To further entice clients to connect, PineAP can advertise previously requested networks.

Basic PineAP configs can be controlled in the following ways:

* **Mimic Open Networks** - toggles PineAP accepting requests for any Wi-Fi network name permitted by filters.
* **Collect Probes** - automatically collect probed networks into the advertisement pool.
* **Advertise Networks** - some clients will not attempt to connect to a network if it is not being actively advertised.
* **Collect Handshakes** - automatically collect WPA-PSK and WPA2-PSK handshake data for offline attacks against the network passphrase.
* **Randomize MAC Address** - randomize the MAC address used in advertising networks from the SSID pool. _(Note: many clients reject networks advertised from random BSSIDs.)_
* **Wigle Mode** - enable Wigle wardriving logs. Requires a USB GPS (see \[\[Wardriving]]).

## PineAP Open AP

To capture clients connecting to unencrypted access points, the Open AP must be enabled.

The Open AP requires a default SSID, however this may be hidden. A hidden SSID does not guarantee that the AP is undiscoverable, and clients that have previously seen the AP before it was hidden will continue to show the name.

By default, the PineAP Open AP uses the hardware address (BSSID) of the Wi-Fi interface in the Pager, but an alternate address can be specified with the BSSID option.

## PineAP Evil WPA

The Pineapple EvilWPA Access Point can be configured to mimic an existing encrypted access point when the encryption key is known.

Additionally, it can be used to capture partial WPA handshakes (**PMKID capture mode**) which may be useful in offline attacks. PMKID and handshake data is saved to `/root/loot/handshakes/` in both **PCAP** and **Hashcat `.22000`** formats.

The EvilWPA AP requires a default SSID, however this may be hidden. As with the Open AP, a hidden SSID does not guarantee the AP is undiscoverable, and clients that previously saw the name will keep showing it. By default EvilWPA uses the Wi-Fi interface's BSSID, with an optional BSSID override.

## PineAP SSID Pool

The PineAP SSID Pool is the list of open networks used when the **Advertise Networks** option is enabled.

* **Max 64 SSIDs** in the pool - the oldest entries expire first.
* Populate it manually, or let **Collect Probes** fill it from nearby probe requests.

## PineAP Filters

There are two filters - a **Network Filter** (by SSID) and a **Client Filter** (by MAC address) - and each runs in **Allow** or **Deny** mode:

* **Allow mode** - only listed entries may associate.
* **Deny mode** - everything _except_ listed entries may associate.

> The defaults are **Allow mode with empty lists**, which blocks _all_ associations. You must add your target(s) (or switch modes) before anything can connect.

Typically both filter types are combined. On an engagement where the target SSIDs are known, set the **Network Filter** to **Allow Mode** and add the target SSIDs to the allow list. At the same time, set the **Client Filter** to **Deny Mode** with an empty filter list, allowing the PineAP Open AP to capture any client attempting to connect to one of the target SSIDs.

### Filter commands (from payloads)

Filter changes take effect immediately.

```
PINEAPPLE_NETWORK_FILTER_ADD | ADD_FILE | DELETE | CLEAR | LIST | MODE [allow|deny]
PINEAPPLE_DEVICE_FILTER_ADD  | ADD_FILE | DELETE | CLEAR | LIST | MODE [allow|deny]
```

(The older `PINEAPPLE_SSID_FILTER_*` names still work.) Mimicry is toggled with `PINEAPPLE_MIMIC_ENABLE` / `PINEAPPLE_MIMIC_DISABLE` (firmware **1.0.5+**).

### SSID pool commands (from payloads)

```
PINEAPPLE_SSID_POOL_ADD "name" | _ADD_FILE | _DELETE | _CLEAR | _LIST
PINEAPPLE_SSID_POOL_COLLECT_START | _COLLECT_STOP
PINEAPPLE_SSID_POOL_START {randomize} | _STOP
```

`_START` requires the Open AP enabled and mimicry on; `_START randomize=true` uses random BSSIDs (which many clients reject).

## PineAP Client List

Finally, you can view the list of clients connected to the Pager on either the PineAP Open or the PineAP EvilWPA access points. From within the client list you can view details and **kick clients** from the access point - doing so automatically adjusts the filters to prevent the client from reconnecting.

## Related commands

* **Deauth:** `DEAUTH_CLIENT [bssid] [target] [channel]` - works on 2.4 GHz and non-DFS 5 GHz only; **PMF/WPA3 and 6 GHz are immune**.
* **Find a client's IP:** `FIND_CLIENT_IP [mac] {timeout}`
* **Channel examination:** `PINEAPPLE_EXAMINE_CHANNEL` / `PINEAPPLE_EXAMINE_BSSID` / `PINEAPPLE_EXAMINE_RESET`
* **Set monitored bands:** `PINEAPPLE_SET_BANDS wlan1mon 2 5 6`
* **New recon session:** `PINEAPPLE_RECON_NEW {name}`
* **Packet capture:** `WIFI_PCAP_START` / `WIFI_PCAP_STOP`

See \[\[Payloads]] for the full command set.
