# Themes

## Pager Themes

The Pager's color UI is skinnable - you can drop in custom themes (backgrounds, colors, boot splash, etc.) to personalize the device.

### Links

* [Themes GitHub repo](https://github.com/hak5/wifipineapplepager-themes)
* [Default `wargames` theme](https://github.com/hak5/wifipineapplepager-themes/tree/master/themes/wargames) - use as a template

## Installing a theme

1.  Put the theme folder(s) under `/mmc/root/themes/` on the device (via `scp`/`sftp` or by cloning directly on the Pager).

    ```bash
    scp -r <theme-folder> root@172.16.52.1:/mmc/root/themes/
    ```
2. Select the theme from the device UI (Settings).

> Remember `/root` and `/mmc/root` are the same location, so `/root/themes/` and `/mmc/root/themes/` refer to the same folder.

## Making your own

* Start from the [`wargames` theme](https://github.com/hak5/wifipineapplepager-themes/tree/master/themes/wargames) as a template and edit it to taste.
* **Background images are `480×222 px`** - match that resolution so artwork isn't scaled or cropped.
* Keep assets small; the device storage and the root overlay are limited (see \[\[General]]).

## Related notes

* \[\[General]] - device hardware and display
* \[\[Payloads]] - scripting the device
