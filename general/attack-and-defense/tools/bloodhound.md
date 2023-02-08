# Bloodhound

## About

[Bloodhound](https://github.com/BloodHoundAD/BloodHound) is "an Attack Path Management solution that continuously maps and quantifies Active Directory Attack Paths. You can remove millions, even billions of Attack Paths within your existing architecture and eliminate the attacker’s easiest, most reliable, and most attractive techniques."

[Bloodhound Docs](https://bloodhound.readthedocs.io/en/latest/index.html)

## Install

Pre-Compiled binaries can be found [here](https://github.com/BloodHoundAD/BloodHound/releases)

Add the neo4j repo to your apt sources (Echoing this out kept fighting me so I nano'd the file myself)

```bash
wget -O - https://debian.neo4j.com/neotechnology.gpg.key | sudo apt-key add -
echo 'deb https://debian.neo4j.com stable 4.4' > /etc/apt/sources.list.d/neo4j.list
sudo apt-get update
```

```bash
sudo nano /etc/apt/sources.list.d/neo4j.list
```

![](<../../../.gitbook/assets/image (100).png>)

Install apt-transport-https and neo4j

```bash
sudo apt install apt-transport-https neo4j
```

Ensure Neo4j runs properly. Stop the service, manually start it and verify no issues prevent it from running

```bash
sudo systemctl stop neo4j
cd /usr/bin
sudo ./neo4j console
```

![](<../../../.gitbook/assets/image (102) (1).png>)

If it start properly, start the service

```bash
sudo systemctl start neo4j
```

Once started, go to: [http://localhost:7474/](https://localhost:7474/) log in with neo4j:neo4j, change the password when prompted.

![](<../../../.gitbook/assets/image (98) (1).png>)

After logging in we should see:

![](<../../../.gitbook/assets/image (103).png>)

Once we have that started, download a Pre-Compiled binary from [here](https://github.com/BloodHoundAD/BloodHound/releases). From inside the unzipped folder we can start Bloodhound.

```bash
sudo ./BloodHound.bin --no-sandbox
```

![](<../../../.gitbook/assets/image (104) (2).png>)

![](<../../../.gitbook/assets/image (99).png>)

Login with neo4j:(password you set), and we're done installing and running.

![](<../../../.gitbook/assets/image (101).png>)

## Usage

This is a screenshot from an example but this is what you \*can\* see

![](<../../../.gitbook/assets/image (2) (1).png>)
