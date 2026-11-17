# Ludus

## About

[Ludus](https://docs.ludus.cloud/docs/intro/) is a system to build easy to use cyber environments, or "ranges" for testing and development. Built on Proxmox, it enables advanced automation while still allowing easy manual modifications or setup of virtual machines and networks. It is implemented as a server that runs Packer and Ansible to create templates and deploy complex cyber environments from a single configuration file. It is accessed via the Ludus CLI (client), the WebUI, or the Proxmox web interface. Normal users should not need to access Ludus via SSH.

### Links

* [Homepage](https://ludus.cloud/)
* [Docs](https://docs.ludus.cloud/docs/intro/)
* [Install Ludus](https://docs.ludus.cloud/docs/quick-start/install-ludus/)
* [Changelog](https://ludus.cloud/changelog)

## Requirements

Ludus does have specific system requirements to be used. I've highlighted some specifics.

<figure><img src="../.gitbook/assets/image (1128).png" alt=""><figcaption></figcaption></figure>

I'm installing mine on an HP EliteDesk DM running [Debian 13](https://www.debian.org/download)) with:

* Intel i5-8500T@ 3.50 GHz
* 32GB RAM
* 1TB NVMe SSD

## Install

To install ludus we will need to be the root user on our Debian machine

```
su -
```

Then we install pre requisites

```
apt update && apt install curl sudo ca-certificates
```

<figure><img src="../.gitbook/assets/image (1129).png" alt=""><figcaption></figcaption></figure>

Now we install Ludus with

```
curl --proto '=https' --tlsv1.2 -sSf https://ludus.cloud/install | bash
```

<figure><img src="../.gitbook/assets/image (1130).png" alt=""><figcaption></figcaption></figure>

We accept the license agreement

<figure><img src="../.gitbook/assets/image (1131).png" alt=""><figcaption></figcaption></figure>

This will ask some questions, have you accept an EULA and go through some setup config. Most, if not all, can be kept default.

<figure><img src="../.gitbook/assets/image (1132).png" alt=""><figcaption></figcaption></figure>

This will also prompt you to make an admin user.

<figure><img src="../.gitbook/assets/image (1133).png" alt=""><figcaption></figcaption></figure>

Then will ask if you're ready to install and proceed when you select yes.

{% hint style="info" %}
This will take some time, so step away for a few. The machine may restart once or twice as well. With the newest install, it pauses for the reboot as to not drop the SSH connection.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1134).png" alt=""><figcaption></figcaption></figure>

Once you see the following, it should be installed.

<figure><img src="../.gitbook/assets/image (1135).png" alt=""><figcaption></figcaption></figure>

We can view our install status, creds, and API key with

```
ludus-install-status
```

<figure><img src="../.gitbook/assets/image (1136).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If running this headless, to set the API key with:
{% endhint %}

```
export LUDUS_API_KEY='API-KEY-HERE'
```

### Adding License Key

If you get a license key or an NFR (Not For Resale) license, we we can add it during install or after install. Your key should look like:

```
46C1CA-B11C52-80E9E7-19E436-FDDG1B-V3
```

You will need to add the key to your Ludus Config file. Mine was under the default of `/opt/ludus/config.yml`. Inside there will be a spot for `license_key:` . Without a key it will be `community`. Remove `community` and paste in your key and save.

Once that is done we run the following to set the Web URL

```
LUDUS_URL=https://LUDUS_MACHINE_IP:8080
```

Then we restart the ludus service

```
systemctl restart ludus
systemctl restart ludus-admin
```

## Sources

### CLI

To view current sources we run:

```
ludus source list
```

We can see what is within a source such as blueprint, templates, and ansible, To view the catalog within a selected source we run:

```
ludus source list ludus-source-bsl --catalog
```

<figure><img src="../.gitbook/assets/image (1137).png" alt=""><figcaption></figcaption></figure>

I'm only going to cover the official ludus source but you can find out more [here on their docs](https://docs.ludus.cloud/docs/using-ludus/sources/).

### Web UI

From the Web UI we can simply click on 'Sources' on the left and view, or add sources.

<figure><img src="../.gitbook/assets/image (1138).png" alt=""><figcaption></figcaption></figure>

To view the catalog from that source, just select the source.

<figure><img src="../.gitbook/assets/image (1139).png" alt=""><figcaption></figcaption></figure>

## Templates

### CLI

We can see what templates are included by default, and if they are built. To view this we run:

```
ludus templates list
```

<figure><img src="../.gitbook/assets/image (1140).png" alt=""><figcaption></figcaption></figure>

To add a template we run

```
ludus source add ludus-source-bsl --templates TEMPLATE-NAME
```

Eg. Debian 13

```
ludus source add ludus-source-bsl --templates debian-13-x64-server-template
```

<figure><img src="../.gitbook/assets/image (1141).png" alt=""><figcaption></figcaption></figure>

To build a template we run:

```
ludus templates build -n debian-13-x64-server-template
```

or we can build them all with:

```
ludus templates build
```

{% hint style="info" %}
This will take some time, so step away for a few. The machine may restart once or twice as well. With the newest install, it pauses for the reboot as to not drop the SSH connection.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1142).png" alt=""><figcaption></figcaption></figure>

To check on the status, this will show us where it's at in the process and when it's finished. We can run:

```
ludus templates logs -f
```

<figure><img src="../.gitbook/assets/image (1143).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1144).png" alt=""><figcaption></figcaption></figure>

I'm only covering what is included with the base ludus, but more info on Templates can be found [here on their docs](https://docs.ludus.cloud/docs/using-ludus/templates).

### WebUI

Selecting `Templates` on the side panel will show us current templates and their status.

<figure><img src="../.gitbook/assets/image (1145).png" alt=""><figcaption></figcaption></figure>

If we want to add more templates, we need to select `Sources` from the side panel then select our source.

<figure><img src="../.gitbook/assets/image (1146).png" alt=""><figcaption></figcaption></figure>

Within here we can see blueprints to build, templates, and ansible roles. Selecting `Templates`, we can check the boxes of the templates we want to add and click install.

{% hint style="info" %}
This will take some time, so step away for a few. This also may fail, but can be selected to be built again.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1147).png" alt=""><figcaption></figcaption></figure>

## Ranges

### CLI

Once your API key exported

```
export LUDUS_API_KEY='USER-API-KEY'
```

See what ranges you have access to, note the `RANGE ID`

```
ludus range accessible
```

View the status of the range

```
ludus range status -r RANGE_ID
```

<figure><img src="../.gitbook/assets/image (1148).png" alt=""><figcaption></figcaption></figure>

## Power

### CLI

```bash
ludus power on/off --name all -r RANGE_ID # Power on/off all range VMs
```

### WebUI

To power on/off the VMs, we either right-click anywhere within the range editor and select `power on/off All VMs` .&#x20;

<figure><img src="../.gitbook/assets/image (1149).png" alt=""><figcaption></figcaption></figure>

Or we can click the three dots in the top right, go to power, and select power on/off.

<figure><img src="../.gitbook/assets/image (1150).png" alt=""><figcaption></figcaption></figure>

