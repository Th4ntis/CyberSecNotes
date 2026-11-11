# Modules

## Modules & Packages

WiFi Pineapple **Modules** allow the interface to be extended to support new community-built features or offer front-ends to command-line tools. A vast library of **Packages** is also available. More info on [their docs page](https://docs.hak5.org/wifi-pineapple/ui-overview/modules).

Modules can be found from the **Puzzle Piece** icon on the left pane. !\[\[Pasted image 20250909133607.png]]

> **Modules vs. Packages:**
>
> * **Modules** are Pineapple apps with a web UI (e.g. Evil Portal). They're published to the device's download site from the Hak5 module repo.
> * **Packages** are plain OpenWRT/Linux command-line tools and drivers (no UI), used from the Web Terminal or SSH.

## Modules

We can select the Modules tab and load what modules are available for installation. Each entry shows its name, description, version, size, and author, plus an **Install/Update** button. !\[\[Pasted image 20250909133610.png]]

To install a module, just select **Install**. !\[\[Pasted image 20250909133614.png]]

Once it's installed it will appear under the **Installed** section (as a card). We can select the **pin** icon to add it to the pane on the left, or open it from here. We can remove it by selecting the **trashcan** icon. !\[\[Pasted image 20250909133617.png]]

Some modules may require additional dependencies; when selecting one, it will take a minute to load and prompt you to install them. !\[\[Pasted image 20250909133622.png]]

Once installed you'll be taken back to the modules main page.

> **Where modules come from:** the official repo is [github.com/hak5/mk7-modules](https://github.com/hak5/mk7-modules/). Community PRs are reviewed and published to the device's download site. Developer docs live at [hak5.github.io/mk7-docs](https://hak5.github.io/mk7-docs/).

## Packages

Packages are provided by the Hak5 and OpenWRT community repositories, and contain a wide range of standard Linux command-line tools. There are A LOT of them, so use the search function to find some, or scroll through the list to grab any that interest you. !\[\[Pasted image 20250909133626.png]]

* Manage/run packages from the **Web Terminal** (terminal icon top-right, or the backtick `` ` `` key) or over **SSH** (`ssh root@172.16.42.1`).
* The underlying package manager is **`opkg`** (OpenWRT), so standard `opkg update` / `opkg install <pkg>` workflows apply from the terminal.

> ⚠️ Space on the Pineapple is limited - install only what you need, and be cautious updating base system packages.

## Related notes

* \[\[Evil Portal]] - a commonly installed module
* \[\[Basics]] - accessing the Web Terminal / SSH
