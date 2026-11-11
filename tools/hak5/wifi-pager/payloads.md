# Payloads

## Pager Payloads

Payloads are written in **DuckyScript** (as bash scripts that call Pager-specific DuckyScript commands). A user payload lives at a path like `/mmc/root/payloads/user/<category>/<payload-name>/payload.sh`.

> **Note on paths:** `/root` and `/mmc/root` are the **same location** on the Pager, so you'll see both spellings. Payloads live under `/root/payloads/` (a.k.a. `/mmc/root/payloads/`), split into `alerts/`, `recon/`, and `user/` subtrees.

### Links

* [Payloads Docs Page](https://docs.hak5.org/wifi-pineapple-pager/payloads-1/)
* [Installing Payloads Docs Page](https://docs.hak5.org/wifi-pineapple-pager/payloads-1/installing-payloads/)
* [Official payloads repo](https://github.com/hak5/wifipineapplepager-payloads/tree/master) - `alert`, `recon`, and `user` categories

## The three payload types

### Alert payloads

Alert payloads are small, typically non-interactive scripts launched in response to conditions in the environment. They can take simple actions like displaying a message, playing a ringtone, or vibrating the device.

Alert payloads run for background events that can happen at any time while the Pineapple is operating:

* WPA handshake capture
* Wi-Fi Denial of Service (deauth flood) detection
* A client connecting to a Pineapple access point
* Authentication details captured by a Pineapple access point

Because they may be launched **repeatedly** as events fire, they should be slim and minimal.

* **Location:** `/root/payloads/alerts/<category>/` - categories mirror the trigger, e.g. `handshake_captured`, `deauth_flood_detected`, `pineapple_client_connected`, `pineapple_client_disconnected`.
* **Alert variables** passed to the script include `$_ALERT`, `$_ALERT_HANDSHAKE_PCAP_PATH`, `$_ALERT_HANDSHAKE_HASHCAT_PATH`, `$_ALERT_CLIENT_CONNECTED_SSID`, and more.

### User payloads

User payloads are the fully-featured big brother to Alert payloads. They are run by the user from the **Payloads** panel of the device dashboard.

User payloads expose the **full range of Pineapple DuckyScript commands**, which lets you build interactions for entering text, IP addresses, MAC addresses, confirming actions, displaying logs and status results, and more.

* **Location:** `/root/payloads/user/<category>/<name>/payload.sh`

### Recon payloads

Recon payloads are run against access points and clients discovered by the Recon process - select a device in the Recon list, then **A → run a Recon payload against it**.

They also use the full range of DuckyScript commands and user interactions, plus **recon context variables** describing the selected target:

* `${_RECON_SELECTED_AP_SSID}`, `${_RECON_SELECTED_AP_BSSID}`, `${_RECON_SELECTED_AP_CHANNEL}`
* `${_RECON_SELECTED_CLIENT_MAC_ADDRESS}`
* `$PAYLOAD_HOME` is available to all payload types.

## Installing payloads

1.  **Get the payloads** - clone or download the repo (git or zip):

    ```bash
    git clone https://github.com/hak5/wifipineapplepager-payloads.git
    ```

    You can also run `git` **directly on the Pager** over SSH.
2.  **Copy them to the Pager** with `scp` or `sftp` (SFTP, not plain FTP) as `root`, using the password you set during setup:

    ```bash
    scp -r <payload-folder> root@172.16.52.1:/mmc/root/payloads/user/<category>/
    ```
3. On **Windows**, make sure files are saved with **Unix (LF) line endings** - CRLF line endings will stop payloads from running.

## Payload rules & tips

* The Pager CPU is **`mipsel`** (MIPS little-endian) - any compiled binary you ship must be built for that architecture.
* A payload needs a `payload.sh`, and any binaries must have the **executable bit** set (`chmod +x`).
*   Install extra packages to the **MMC** (the root overlay has < 32 MB free):

    ```bash
    opkg install -d mmc python3
    ```
* **Do not** update the base system packages - it can break firmware.

## Pager DuckyScript command reference

DuckyScript commands are written in ALL CAPS. The Pager adds UI and hardware commands on top of standard DuckyScript:

**User-interaction / dialog**

| Command                                         | Purpose                                                              |
| ----------------------------------------------- | -------------------------------------------------------------------- |
| `ALERT [message]`                               | Show an alert message.                                               |
| `CONFIRMATION_DIALOG [prompt]`                  | Yes/no dialog - returns `1` (continue) or `0` (cancel).              |
| `ERROR_DIALOG [text]`                           | Show an error.                                                       |
| `PROMPT [message]`                              | Display a prompt.                                                    |
| `IP_PICKER [prompt] [default IP]`               | Prompt for an IP address.                                            |
| `MAC_PICKER [prompt] [default mac]`             | Prompt for a MAC.                                                    |
| `NUMBER_PICKER [prompt] [default]`              | Prompt for a number.                                                 |
| `TEXT_PICKER [prompt] [default]`                | Prompt for text.                                                     |
| `LIST_PICKER [title] [option] [default]`        | Pick from a list (firmware **1.0.8+**).                              |
| `LOG [color] [message]`                         | Write a colored log line.                                            |
| `START_SPINNER [message]` / `STOP_SPINNER {id}` | Progress spinner.                                                    |
| `WAIT_FOR_BUTTON_PRESS [button]`                | Block for a button (`ANY`, `A`, `B`, `UP`, `DOWN`, `LEFT`, `RIGHT`). |
| `WAIT_FOR_INPUT`                                | Block for input.                                                     |

**Hardware / feedback**

| Command                                  | Purpose                                                                             |
| ---------------------------------------- | ----------------------------------------------------------------------------------- |
| `RINGTONE {vibrate} [rtttl or filename]` | Play a ringtone (looks in `/root/ringtones/`; built-ins in `/lib/pager/ringtones`). |
| `VIBRATE [rtttl or filename]`            | Vibrate.                                                                            |
| `LED` / `DPADLED_CONFIG`                 | Control the RGB LEDs.                                                               |
| `ENABLE_DISPLAY` / `DISABLE_DISPLAY`     | Toggle the screen.                                                                  |
| `BATTERY_CHARGING` / `BATTERY_PERCENT`   | Query battery state.                                                                |

**Config store (persists across firmware upgrades)**

* `PAYLOAD_GET_CONFIG`, `PAYLOAD_SET_CONFIG`, `PAYLOAD_DEL_CONFIG`

**Example**

```bash
__userip=$(IP_PICKER "Target IP" "1.2.3.4") || exit 0
```

PineAP, Wi-Fi, deauth, GPS and Wigle commands are also available from payloads - see \[\[PineAP]] and \[\[Wardriving]].
