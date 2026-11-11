# Wardriving

## Wardriving with the Pineapple Pager

We can use the pager to do some nice wardriving, but to have GPS with it, we have a couple options: using the [Glytch GPS Module](https://shop.hak5.org/products/glytch-gps-mod-for-pager) or [Mobile2GPS](https://github.com/ryanpohlner/mobile2gps).

> **How wardriving works on the Pager:** once a GPS fix is available, enabling **Wigle Mode** tags every device Recon sees with GPS coordinates and writes a **Wigle-ready `.csv`** to `/root/loot/wigle/`. You then upload those files to [WiGLE](https://wigle.net). The Pager never contacts WiGLE unless you explicitly log in and upload.

> **GPS basics on the Pager:** GPS receivers plug into the **USB-A port** and appear as serial devices (`ttyUSBx` / `ttyACMx`). A cold fix with a clear view of the sky takes **\~15–30 minutes**. You can verify a lock on-device under `Settings → GPS`, or over SSH with `cgps`. Supported baud rates are 4800 / 9600 / 115200; after changing GPS settings, choose **Restart GPSd**.

## Glytch GPS Module

This is form fitting and simple to use, but it does cover the USB-C port so we are unable to charge it. With the Module plugged in, we go to `Settings -> GPS -> Serial Device -> Select TTYUSB0` and that's it. Pretty straight forward. The GPS is very weak inside from my experience, so it may not show your coordinates immediately.

> If `ttyUSB0` doesn't appear, the GPS may enumerate under a USB _path_ ID instead. You can confirm the device with:
>
> ```bash
> ls -l /dev/serial/by-path/
> ```
>
> and check live NMEA/fix data with `cgps`.

## Mobile2GPS

This is my preferred way to go as it's super easy, leave the USB-C port open, and makes the pager easier to carry. To start we need to connect our pager to our machine so we can either SSH into it or access the Virtual Pager at http://172.16.52.1:1471 .

> **Heads-up on addressing:** the Pager lives on `172.16.52.0/24`. The Virtual Pager UI is `http://172.16.52.1:1471`, SSH is `root@172.16.52.1`. (If you've seen `172.16.51.1` in older notes, that's a typo - it's always `.52.`.)

We will need to have the Management AP setup for our phone to connect to. To ensure this is setup we go to: `Settings -> Network -> Management AP Setup`. !\[\[Pasted image 20260220124736.png]]

Give it a network name, setup the encryption type, and the passphrase.

> From a payload/SSH you can do the same thing with:
>
> ```bash
> WIFI_MGMT_AP wlan0mgmt 'PagerManagement' sae-mixed 'SuperSecret_PagerPassword'
> ```
>
> (`sae-mixed` = WPA2/WPA3 mixed; use `psk2` for WPA2-only.)

We need to clone the repository if you're on MacOS or Linux, you can either download and extract the .zip file or use `git`. Also download the mobile2gps binary from the [releases page](https://github.com/ryanpohlner/mobile2gps/releases/) or with `wget`.

```bash
git clone https://github.com/ryanpohlner/mobile2gps.git && cd mobile2gps

wget https://github.com/ryanpohlner/mobile2gps/releases/download/v1.6/mobile2gps
```

!\[\[Pasted image 20260220130945.png]]

From here we need to make the `mobile2gps` directory on our pager under `/mmc/root/payloads/user/general/`. Through SSH or the Virtual Pager:

```bash
mkdir /mmc/root/payloads/user/general/mobile2gps
```

!\[\[Pasted image 20260220130531.png]]

Now we need to move the following files to our pager:

* payload.sh
* mobile2gps
* index.html

Using `scp` or [WinSCP](https://winscp.net/eng/download.php) if you're on Windows.

```bash
scp payload.sh root@172.16.52.1:/mmc/root/payloads/user/general/mobile2gps/
scp mobile2gps root@172.16.52.1:/mmc/root/payloads/user/general/mobile2gps/
scp index.html root@172.16.52.1:/mmc/root/payloads/user/general/mobile2gps/
```

> **Windows tip:** make sure `payload.sh` keeps **Unix (LF) line endings**, and that the `mobile2gps` binary stays executable (`chmod +x mobile2gps` on the Pager) - CRLF endings or a missing exec bit will stop the payload from running.

!\[\[Pasted image 20260220131058.png]]

Make sure our phone is connected to our Management AP. On the pager go to: `Payloads -> general -> mobile2gps -> Launch`. !\[\[Pasted image 20260220125040.png]]

Once here, press the Up Arrow to start the server for the GPS. !\[\[Pasted image 20260220125128.png]]

Now on our phone we go to: https://172.16.52.1:1993 and press `Start`. !\[\[signal-2026-02-20-131458.png]]

On the pager we can press the right arrow to verify we have GPS coordinates. !\[\[Pasted image 20260220125336.png]]

We can also verify by going to: `Settings -> GPS`. !\[\[Pasted image 20260220125442.png]]

From here, we can start recon mode, press the Green button and go down to enable `Wigle Mode`. This will save a wigle ready .csv file for us to use. !\[\[Pasted image 20260220125611.png]] !\[\[Pasted image 20260220125628.png]]

Now we can either get the files off of our Pager using `scp` (or WinSCP) to upload to Wigle. OR we can use the [wigle-toolkit](https://github.com/hak5/wifipineapplepager-payloads/blob/master/library/user/exfiltration/wigle-toolkit/payload.sh) payload. This will upload our Wigle `.csv` files from `/mmc/root/loot/wigle/`.

## Uploading to WiGLE from the device

Instead of pulling files off manually, you can log in and upload straight from the Pager (via a payload or SSH) with the built-in Wigle commands:

```
WIGLE_LOGIN {username} {password}
WIGLE_START
WIGLE_STOP
WIGLE_UPLOAD {--archive} {--remove} [path]
WIGLE_LOGOUT
```

* `--archive` moves uploaded logs to `/root/loot/archive/wigle/`.
* `--remove` deletes them after a successful upload.
* Logs are written to `/root/loot/wigle/` (same as `/mmc/root/loot/wigle/`).

## Related notes

* \[\[General]] - device + USB-A GPS port
* \[\[PineAP]] - Wigle Mode toggle lives alongside PineAP config
* \[\[Payloads]] - payload structure and installation
