# Hashcat

### About

Hashcat is a free powerful open-source hash cracking tool. From their github "hashcat is the world's fastest and most advanced password recovery utility, supporting five unique modes of attack for over 300 highly-optimized hashing algorithms. hashcat currently supports CPUs, GPUs, and other hardware accelerators on Linux, Windows, and macOS, and has facilities to help enable distributed password cracking."

hashcat has a lot of additional and helpful tools as well as ZerBea has made some helpful tools as well.

### Links

[Hashcat Homepage](https://hashcat.net/hashcat/) [Hashcat Github](https://github.com/hashcat/hashcat) [HCXTools Github](https://github.com/ZerBea/hcxtools)

### HCXTools

From their github "Small set of tools convert packets from captures (h = hash, c = capture, convert and calculate candidates, x = different hashtypes) for the use with latest hashcat or John the Ripper. The tools are 100% compatible to hashcat and John the Ripper and recommended by hashcat. This branch is pretty closely synced to hashcat git and John the Ripper git."

## Install

You can download their binaries or sources from their homepage or compile from source on linux.

### Hashcat

```
cd /opt/
sudo git clone https://github.com/hashcat/hashcat && cd hashcat
sudo make
sudo make install
```

### Hashcat-Utils

```
cd /opt/
sudo git clone https://github.com/hashcat/hashcat-utils.git && cd hashcat-utils/src
sudo make
sudo cp *bin ../bin
```

### HCXTools

```
sudo apt install libcurl4-openssl-dev libssl-dev zlib1g-dev
cd /opt/
sudo git clone https://github.com/ZerBea/hcxtools.git && cd hcxtools
sudo make
sudo make install
```

## Usage

#### General

Hashcat can be used in many forms but the usual format I follow is:

```
hashcat (attackmode) (hashtype) (workload profile) (hashfile)
```

Example: `hashcat -a # -m # -w # CrackMe.txt`

The types of attackmodes are:

| #                                                                                                                                                                                         | Mode                   |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- |
| 0                                                                                                                                                                                         | Straight               |
| 1                                                                                                                                                                                         | Combination            |
| 3                                                                                                                                                                                         | Bruteforce             |
| 6                                                                                                                                                                                         | Hybrid - Wordlist+Mask |
| 7                                                                                                                                                                                         | Hybrid - Mask+Wordlist |
| 9                                                                                                                                                                                         | Association            |
| To pick up a draggable item, press the space bar. While dragging, use the arrow keys to move the item. Press space again to drop the item in its new position, or press escape to cancel. |                        |

To pick up a draggable item, press the space bar. While dragging, use the arrow keys to move the item. Press space again to drop the item in its new position, or press escape to cancel.

The types of attackmodes are:

* Straight - Tries the exact words that are in your chosen wordlist(s), with no modifications other than rules.
* Combination(Combinator) - Combines the current word with the rest of the words in the wordlist.

If your wordlist was: aa bb cc dd

It would generate hashes for the keys: aabb, aacc, aadd, bbcc, bbdd, ccdd, with no modifications other than rules.

* Brute-Force - Tries all combinations from a given Keyspace. It is the easiest of all the attacks.
* Hybrid Wordlist+Mask - "The hybrid attack is just a [Combinator attack](https://hashcat.net/wiki/doku.php?id=combinator_attack). One side is simply a dictionary, the other is the result of a [Brute-Force attack](https://hashcat.net/wiki/doku.php?id=brute_force_attack). In other words, the full Brute-Force keyspace is either appended or prepended to each of the words from the dictionary. Hence the name, “hybrid”."
* Hybrid Mask+Wordlist - Same as "Hybrid Mask+Wordlist" above but swapped.
* Association - This attack is not yet ready. More info can be found [here](https://hashcat.net/forum/thread-9534.html).

There are a lot of hashtypes so I won't try to list them here but these can be found with `hashcat --help | less` and running down till we find the list. We can also grep for specific hash types as well. `hashcat --help | grep NTLM`.

The workload profile is something we use to speed up the process but can make it so the rest of the computer is slow as it uses much more processing power. Workload Profile types are:

| #                                                                                                                                                                                         | Performance | Runtime | Power Consumption | Impact       |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- | ------- | ----------------- | ------------ |
| 1                                                                                                                                                                                         | Low         | 2ms     | Low               | Minimal      |
| 2                                                                                                                                                                                         | Default     | 12ms    | Economic          | Noticeable   |
| 3                                                                                                                                                                                         | High        | 96ms    | High              | Unresponsive |
| 4                                                                                                                                                                                         | Nightmare   | 480ms   | Insane            | Headless     |
| To pick up a draggable item, press the space bar. While dragging, use the arrow keys to move the item. Press space again to drop the item in its new position, or press escape to cancel. |             |         |                   |              |

To pick up a draggable item, press the space bar. While dragging, use the arrow keys to move the item. Press space again to drop the item in its new position, or press escape to cancel.

#### Dictionary

If we want to use a dictionary attack, like using `rockyou.txt` for example

```
hashcat -a 0 -w 3 -m 22000 -w 3(hash file) (wordlist)
```

Depending on your hardware, the dictionary you chose, and the password, this may take some time. You can press S for a status to see the time time estimated on finishing, as well as the updated "Recovered.Total" to see the recovered keys"

We can run the same command again with --show appended to the end to see our cracked passwords.

#### Brute Force

If we wanted to run a brute force attack rather than a dictionary attack, it's a similar command

```
hashcat -a 3 -w 3 -m 22000 -w 3 (hash file) '?l?l?l?l?l?l?l'
```

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

## Quick References

#### NTLM:

```bash
hashcat -m 1000 ntlm-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 -w 3 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

#### NTLMv2:

```bash
hashcat -m 5600 ntlmv2-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 -w 3 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

#### Kerberoast:

```bash
hashcat -m 13100 kerb-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 -w 3 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

#### AS-REP:

```bash
hashcat -m 18200 asrep-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

#### WPA/PMKID

```bash
hashcat -m 22000 wpa-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```
