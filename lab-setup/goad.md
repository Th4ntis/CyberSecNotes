# GOAD

## About

### [GOAD](https://orange-cyberdefense.github.io/GOAD/)

[Game Of Active Directory](https://orange-cyberdefense.github.io/GOAD/) is a free pentest active directory LAB(s) project. The purpose of this tool is to give pentesters a vulnerable Active directory environment ready to use to practice usual attack techniques. The idea behind this project is to give you an environment where you can try and train your pentest skills without having the pain to build all by yourself.

### Links

[Install Ludus](https://docs.ludus.cloud/docs/quick-start/install-ludus/)

[Ludus-GOAD Guide](https://docs.ludus.cloud/docs/environment-guides/goad/)

## Installing

Once Ludus is installed

1. Clone the GOAD repository

```
git clone https://github.com/Orange-Cyberdefense/GOAD.git && cd GOAD
```

3. Start GOAD, check that everything is set with no errors, and install. This will take a long time.

```
./goad.sh -p ludus
```

4. Exit GOAD and update `/root/.goad/goad.ini` with your users API key, then install

```
GOAD/ludus/local > check
GOAD/ludus/local > set_lab XXX # GOAD/GOAD-Light/NHA/SCCM
GOAD/ludus/local > install
```

<figure><img src="../.gitbook/assets/image (1111).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1112).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1113).png" alt=""><figcaption></figcaption></figure>

I did have a couple error that stopped the install, so added the API of my admin user key to `/root/.goad/goad.ini` then started the install again.

```
./goad.sh -p ludus
GOAD/ludus/local > install
```

<figure><img src="../.gitbook/assets/image (1114).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1115).png" alt=""><figcaption></figcaption></figure>

Then once more when it was using the API key from the environment and deploying So I had to load the instance from within GOAD.

```
./goad.sh
GOAD/ludus/local > ls
GOAD/ludus/local > load (INSTANCE-ID)
GOAD/ludus/local > install
```

<figure><img src="../.gitbook/assets/image (1116).png" alt=""><figcaption></figcaption></figure>

## Kali VM with Ludus and GOAD

1. Find the GOAD UserID

```
ludus users list all
```

<figure><img src="../.gitbook/assets/image (1117).png" alt=""><figcaption></figcaption></figure>

2. Get the `config.yml` file

```
ludus --user GOAD-USERID range config get > basic-config.yml
```

<figure><img src="../.gitbook/assets/image (1118).png" alt=""><figcaption></figcaption></figure>

3. Edit the `basic-config.yml` file with the following added to the bottom

```yaml
  - vm_name: "{{ range_id }}-kali"
    hostname: "{{ range_id }}-kali"
    template: kali-x64-desktop-template
    vlan: 10
    ip_last_octet: 99
    ram_gb: 4
    cpus: 4
    linux: true
    testing:
      snapshot: false
      block_internet: false
```

4. Set the new config file and deploy it

```
ludus --user GOAD-USERID range config set -f basic-config.yml
ludus --user GOAD-USERID range deploy -t vm-deploy
```

5. Check on the deployment process

```
ludus --user GOAD-USERID range logs -f
```

<figure><img src="../.gitbook/assets/image (1119).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1120).png" alt=""><figcaption></figcaption></figure>

6. Deploy the Kali VM

```
ludus --user GOAD-USERID range deploy --limit localhost,GOAD-USERID-kali
```

<figure><img src="../.gitbook/assets/image (1121).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1122).png" alt=""><figcaption></figcaption></figure>

7. Verify all VMs with their status

```
ludus --user GOAD-USERID range status
```

<figure><img src="../.gitbook/assets/image (1123).png" alt=""><figcaption></figcaption></figure>

8\. If the machines are offline we can start them with

```
ludus --user GOADe202d2 range deploy
```

9. Get Wireguard configuration file

```
ludus user wireguard | tee ludus.conf
```

<figure><img src="../.gitbook/assets/image (1125).png" alt=""><figcaption></figcaption></figure>

9. Save the file as a `.conf` file and use Wireguard to connect to it. Once connected, access your Kali machine via GUI in the browser, over SSH.

```
sudo wg-quick up GOAD.conf
```

<figure><img src="../.gitbook/assets/image (1126).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1127).png" alt=""><figcaption></figcaption></figure>
