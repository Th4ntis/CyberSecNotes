# GOAD

## Installing

Once we have [installed Ludus](ludus.md) onto our machine, we can proceed with installing [Game of Active Directory (GOAD)](https://orange-cyberdefense.github.io/GOAD). This will give us a great environment to attack, test tools against, and more.

### CLI

To install GOAD via CLI we need to add the source first. Pressing space to select `Game of Active Directory (GOAD)`, then press `enter`.

```
ludus source add ludus-source-bsl
```

<figure><img src="../.gitbook/assets/image (1151).png" alt=""><figcaption></figcaption></figure>

Create the range, user, and select the blueprint

```
ludus range create -r GOAD --name GOAD --user th4ntis-ludus --from-blueprint ludus-source-bsl/goad
```

Then deploy the range.

```
ludus range deploy -r GOAD
```

{% hint style="info" %}
This will take some time, so step away for a few. This also may fail, but can be selected to be deployed again.
{% endhint %}

We can view the deploy progress with:

```
ludus range logs -f -r GOAD
```

### Web UI

Installing GOAD from the source blueprints, we simply select `Sources`, select the `Ludus Source - Bad Sector Labs` source.

<figure><img src="../.gitbook/assets/image (1152).png" alt=""><figcaption></figcaption></figure>

To install GOAD we select `Blueprints`, then check box, and hit install.

<figure><img src="../.gitbook/assets/image (1153).png" alt=""><figcaption></figcaption></figure>

Now we go to Ranges and make a new one, and name it. I went with GOAD, then select `Create Range`

<figure><img src="../.gitbook/assets/image (1154).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1155).png" alt=""><figcaption></figcaption></figure>

Now select `Blueprints` from the side panel, and you should see `Game of Active Directory (GOAD)`. Select the 3 dots and apply it to a range.

<figure><img src="../.gitbook/assets/image (1156).png" alt=""><figcaption></figcaption></figure>

Select the Target Range we created, and select `Apply Blueprint`.

<figure><img src="../.gitbook/assets/image (1157).png" alt=""><figcaption></figcaption></figure>

This will take us right into our range, and give us a run down of configuration canvas and show us the layout. From here, to deploy the range, we select the Play button icon in the top right. This will take some time.

{% hint style="info" %}
This will take some time, so step away for a few. This also may fail, but can be selected to be deployed again.
{% endhint %}

<figure><img src="../.gitbook/assets/image (1158).png" alt=""><figcaption></figcaption></figure>

## Connection

Now that GOAD is installed and running, we need to access it. We can do this by getting the WireGuard config.

### CLI

With our API key exported, we can run:

```
ludus user wireguard | tee ludus.conf
```

<figure><img src="../.gitbook/assets/image (1159).png" alt=""><figcaption></figcaption></figure>

From here, we copy/paste that into a new.conf file.

### Web UI

When on any page, we can select our name in bottom right, then `WireGuard Config`

<figure><img src="../.gitbook/assets/image (1160).png" alt=""><figcaption></figcaption></figure>

With that, we can either copy or download it.

<figure><img src="../.gitbook/assets/image (1161).png" alt=""><figcaption></figcaption></figure>

From our machine we use the .conf file to connect to the environment. For Linux it's under `/etc/wireguard/` so we can run:

```
sudo mv wireguard.conf /etc/wireguard/wireguard.conf
```

## Access

We now connect to the Kali machine (or the other machines) with

```
sudo wg-quick up wireguard
```

<figure><img src="../.gitbook/assets/image (1162).png" alt=""><figcaption></figcaption></figure>

We verify by pinging our Kali machine.

<figure><img src="../.gitbook/assets/image (1163).png" alt=""><figcaption></figcaption></figure>

From here, we can SSH to the machine or if we want a GUI we can go to `https://10.1.10.99:8444` and login with `kali:kali`

<figure><img src="../.gitbook/assets/image (1164).png" alt=""><figcaption></figcaption></figure>

## Power

### CLI

```bash
ludus power on/off --name all -r RANGE_ID # Power on/off all range VMs
```

### WebUI

To power on/off the VMs, we either right-click anywhere within the range editor and select `power on/off All VMs` .&#x20;

<figure><img src="../.gitbook/assets/image (1165).png" alt=""><figcaption></figcaption></figure>

Or we can click the three dots in the top right, go to power, and select power on/off.

<figure><img src="../.gitbook/assets/image (1166).png" alt=""><figcaption></figcaption></figure>
