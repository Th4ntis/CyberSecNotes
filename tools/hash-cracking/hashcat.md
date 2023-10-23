# Hashcat

## About

Hashcat is a free powerful open-source hash cracking tool. From their github "**hashcat** is the world's fastest and most advanced password recovery utility, supporting five unique modes of attack for over 300 highly-optimized hashing algorithms. hashcat currently supports CPUs, GPUs, and other hardware accelerators on Linux, Windows, and macOS, and has facilities to help enable distributed password cracking."

hashcat has a lot of additional and helpful tools as well as ZerBea has made some helpful tools as well.

[Hashcat Homepage](https://hashcat.net/hashcat/)

[Hashcat Github](https://github.com/hashcat/hashcat)

### HCXTools

From their github "Small set of tools convert packets from captures (h = hash, c = capture, convert and calculate candidates, x = different hashtypes) for the use with latest hashcat or John the Ripper. The tools are 100% compatible to hashcat and John the Ripper and recommended by hashcat. This branch is pretty closely synced to hashcat git and John the Ripper git."

[HCXTools Github](https://github.com/ZerBea/hcxtools)

## Install

You can download their binaries or sources from their homepage or compile from source on linux.

### Hashcat

`cd /opt/`

`sudo git clone https://github.com/hashcat/hashcat && cd hashcat`

`sudo make`

`sudo make install`

### Hashcat-Utils

`cd /opt/`

`sudo git clone https://github.com/hashcat/hashcat-utils.git && cd hashcat-utils/src`

`sudo make`

`sudo cp *bin ../bin`

### HCXTools

`sudo apt install libcurl4-openssl-dev libssl-dev zlib1g-dev`

`cd /opt/`

`sudo git clone https://github.com/ZerBea/hcxtools.git && cd hcxtools`

`sudo make`

`sudo make install`

## Usage

### General

hashcat can be used in many forms but the usual format I follow is:

hashcat (attackmode) (hashtype) (workload profile) (hashfile)

Example: `hashcat -a # -m # -w # CrackMe.txt`

The types of attackmodes are:

<table><thead><tr><th width="150" align="center">#</th><th align="center">Mode</th><th data-hidden></th></tr></thead><tbody><tr><td align="center">0</td><td align="center">Straight</td><td></td></tr><tr><td align="center">1</td><td align="center">Combination</td><td></td></tr><tr><td align="center">3</td><td align="center">Brute-Force</td><td></td></tr><tr><td align="center">6</td><td align="center">Hybrid Wordlist+Mask</td><td></td></tr><tr><td align="center">7</td><td align="center">Hyrbid Mask+Wordlist</td><td></td></tr><tr><td align="center">9</td><td align="center">Association</td><td></td></tr></tbody></table>

* Straight - Tries the exact words that are in your chosen wordlist(s), with no modifications other than rules.
* Combination(Combinator) - Combines the current word with the rest of the words in the wordlist.

If your wordlist was:

aa

bb

cc

dd

It woud generate hashes for the keys: aabb, aacc, aadd, bbcc, bbdd, ccdd, with no modifications other than rules.

* Brute-Force - Tries all combinations from a given Keyspace. It is the easiest of all the attacks.
* Hybrid Wordlist+Mask - "The hybrid attack is just a [Combinator attack](https://hashcat.net/wiki/doku.php?id=combinator\_attack). One side is simply a dictionary, the other is the result of a [Brute-Force attack](https://hashcat.net/wiki/doku.php?id=brute\_force\_attack). In other words, the full Brute-Force keyspace is either appended or prepended to each of the words from the dictionary. Hence the name, “hybrid”."
* Hybrid Mask+Wordlist - Same as "Hybrid Mask+Wordlist" above but swapped.
* Association - This attack is not yet ready. More info can be found [here](https://hashcat.net/forum/thread-9534.html).

There are a lot of hashtypes so I won't try to list them here but these can be found with `hashcat --help | less` and running down till we find the list. We can also grep for specific hash types as well. `hashcat --help | grep NTLM`.

![](<../../.gitbook/assets/image (290).png>)

The workload profile is something we use to speed up the process but can make it so the rest of the computer is slow as it uses much more processing power. Workload Profile types are:

<table><thead><tr><th width="150" align="center">#</th><th width="150" align="center">Performance</th><th width="150" align="center">Runtime</th><th width="150" align="center">Power Consumption</th><th align="center">Impact</th></tr></thead><tbody><tr><td align="center">1</td><td align="center">Low</td><td align="center">2ms</td><td align="center">Low</td><td align="center">Minimal</td></tr><tr><td align="center">2</td><td align="center">Default</td><td align="center">12ms</td><td align="center">Economic</td><td align="center">Noticeable</td></tr><tr><td align="center">3</td><td align="center">High</td><td align="center">96ms</td><td align="center">High</td><td align="center">Unresponsive</td></tr><tr><td align="center">4</td><td align="center">Nightmare</td><td align="center">480ms</td><td align="center">Insane</td><td align="center">Headless</td></tr></tbody></table>

### Dictionary

If we want to use a dictionary attack, like using `rockyou.txt` for example

`hashcat -a 0 -w 3 -m 22000 -w 3(hash file) (wordlist)`

![](<../../.gitbook/assets/image (358).png>)

![](<../../.gitbook/assets/image (21) (1) (3).png>)

Depending on your hardware, the dictionary you chose, and the password, this may take some time. You can press S for a status to see the time time estimated on finishing, as well as the updated "Recovered.Total" to see the recovered keys"

We can run the same command again with --show appended to the end to see our cracked passwords.

![](<../../.gitbook/assets/image (282).png>)

### Brute Force

If we wanted to run a brute force attack rather than a dictionary attack, it's a similar command

`hashcat -a 3 -w 3 -m 22000 -w 3 (hash file) '?l?l?l?l?l?l?l'`

Replace the `?l` with whatever we deem fit.

* ?l = a-z
* ?u = A-Z
* ?d = 0-9
* ?h = 0-9a-f
* ?H = 0-9A-F
* ?s = !"#$%&'()\*+,-./:;<=>?@\[]^\_\`{|}\~
* ?a = ?l?u?d?s
* ?b = 0x00 - 0xff

This will cover the basics of the hash cracking with hashcat but it can get SO much more advanced with hashcat.
