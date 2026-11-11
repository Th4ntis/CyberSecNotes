# Ludus

## About

[Ludus](https://docs.ludus.cloud/docs/intro/) is a system to build easy to use cyber environments, or "ranges" for testing and development. Built on Proxmox, it enables advanced automation while still allowing easy manual modifications or setup of virtual machines and networks. It is implemented as a server that runs Packer and Ansible to create templates and deploy complex cyber environments from a single configuration file. It is accessed via the Ludus CLI (client), the WebUI, or the Proxmox web interface. Normal users should not need to access Ludus via SSH.

### Links

[Homepage](https://ludus.cloud/)

[Docs](https://docs.ludus.cloud/docs/intro/)

[Install Ludus](https://docs.ludus.cloud/docs/quick-start/install-ludus/)

[Changelog](https://ludus.cloud/changelog)

## Requirements

Ludus does have specific system requirements to be used. I've highlighted some specifics.

<figure><img src="../.gitbook/assets/image (1084).png" alt=""><figcaption></figcaption></figure>

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

Now we install Ludus with

```
curl --proto '=https' --tlsv1.2 -sSf https://ludus.cloud/install | bash
```

<figure><img src="../.gitbook/assets/image (1085).png" alt=""><figcaption></figcaption></figure>

This will ask some questions, have you accept an EULA and go through some setup config. Most, if not all, can be kept default.

<figure><img src="../.gitbook/assets/image (1086).png" alt=""><figcaption></figcaption></figure>

This will also prompt you to make an admin user.

<figure><img src="../.gitbook/assets/image (1087).png" alt=""><figcaption></figcaption></figure>

Then will ask if you're ready to install and proceed when you select yes. This the machine WILL restart twice as it says. Give this some time can come back later.&#x20;

<figure><img src="../.gitbook/assets/image (1088).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1089).png" alt=""><figcaption></figcaption></figure>

After it's been a bit we can SSH back into our machine and from a root session check the install status with:

```
ludus-install-status
```

This will give us logs of what is happening while installing. Running this again when it's finished you will get a list of information you will need.

<figure><img src="../.gitbook/assets/image (1090).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1091).png" alt=""><figcaption></figcaption></figure>

NOTE: If running this headless, to set the API key with:

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

<figure><img src="../.gitbook/assets/image (1092).png" alt=""><figcaption></figcaption></figure>

I'm only going to cover the official ludus source but you can find out more [here on their docs](https://docs.ludus.cloud/docs/using-ludus/sources/).

### Web UI

From the Web UI we can simply click on 'Sources' on the left and view, or add sources.

<figure><img src="../.gitbook/assets/image (1093).png" alt=""><figcaption></figcaption></figure>

To view the catalog from that source, just select the source.

<figure><img src="../.gitbook/assets/image (1094).png" alt=""><figcaption></figcaption></figure>

## Templates

### CLI

We can see what templates are included by default, and if they are built. To view this we run:

```
ludus templates list
```

<figure><img src="../.gitbook/assets/image (1095).png" alt=""><figcaption></figcaption></figure>

To add a template we run

```
ludus source add ludus-source-bsl --templates TEMPLATE-NAME
```

Eg. Debian 13

```
ludus source add ludus-source-bsl --templates debian-13-x64-server-template
```

<figure><img src="../.gitbook/assets/image (1096).png" alt=""><figcaption></figcaption></figure>

To build a template we run:

```
ludus templates build -n debian-13-x64-server-template
```

or we can build them all, **This will take some time**

```
ludus templates build
```

<figure><img src="../.gitbook/assets/image (1097).png" alt=""><figcaption></figcaption></figure>

To check on the status, this will show us where it's at in the process and when it's finished. We can run:

```
ludus templates logs -f
```

<figure><img src="../.gitbook/assets/image (1098).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1099).png" alt=""><figcaption></figcaption></figure>

I'm only covering what is included with the base ludus, but more info on Templates can be found [here on their docs](https://docs.ludus.cloud/docs/using-ludus/templates).

### WebUI

Selecting `Templates` on the side panel will show us current templates and their status.

<figure><img src="../.gitbook/assets/image (1100).png" alt=""><figcaption></figcaption></figure>

If we want to add more templates, we need to select `Sources` from the side panel then select our source.

<figure><img src="../.gitbook/assets/image (1101).png" alt=""><figcaption></figcaption></figure>

Within here we can see blueprints to build, templates, and ansible roles. Selecting `Templates`, we can check the boxes of the templates we want to add and click install.

<figure><img src="../.gitbook/assets/image (1102).png" alt=""><figcaption></figcaption></figure>

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

## Power

### CLI

```bash
ludus power on/off --name all -r RANGE_ID # Power on/off all range VMs
```

### WebUI

## GOAD

### CLI

To install GOAD via CLI we need to add the source first. Pressing space to select `Game of Active Directory (GOAD)`, then press `enter`.

```
ludus source add ludus-source-bsl
```

<figure><img src="../.gitbook/assets/image (1103).png" alt=""><figcaption></figcaption></figure>

Create the range, user, and select the blueprint

```
ludus range create -r GOAD --name GOAD --user th4ntis-ludus --from-blueprint ludus-source-bsl/goad
```

Then deploy the range.

```
ludus range deploy -r GOAD
```

We can view the deploy progress with:

```
ludus range logs -f -r GOAD
```

### Web UI

Installing GOAD from the source blueprints, we simply select `Sources`, select the `Ludus Source - Bad Sector Labs` source.

<figure><img src="../.gitbook/assets/image (1104).png" alt=""><figcaption></figcaption></figure>

To install GOAD we select `Blueprints`, then check box, and hit install.

<figure><img src="../.gitbook/assets/image (1105).png" alt=""><figcaption></figcaption></figure>

Now we go to Ranges and make a new one, and name it. I went with GOAD, then select `Create Range` .

<figure><img src="../.gitbook/assets/image (1106).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1107).png" alt=""><figcaption></figcaption></figure>

Now select `Blueprints` from the side panel, and you should see `Game of Active Directory (GOAD)`. Select the 3 dots and apply it to a range.

<figure><img src="../.gitbook/assets/image (1108).png" alt=""><figcaption></figcaption></figure>

Select the Target Range we created, and select `Apply Blueprint`.

<figure><img src="../.gitbook/assets/image (1109).png" alt=""><figcaption></figcaption></figure>

This will take us right into our range, and give us a run down of configuration canvas and show us the layout. From here, to deploy the range, we select the Play button icon in the top right. This will take some time.

<figure><img src="../.gitbook/assets/image (1110).png" alt=""><figcaption></figcaption></figure>
