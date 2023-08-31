# JohnTheRipper

## About

From the github "John the Ripper is a fast password cracker, currently available for many flavors of Unix, macOS, Windows, DOS, BeOS, and OpenVMS (the latter requires a contributed patch). Its primary purpose is to detect weak Unix passwords. Besides several crypt(3) password hash types most commonly found on various Unix flavors, supported out of the box are Kerberos/AFS and Windows LM hashes, as well as DES-based tripcodes, plus hundreds of additional hashes and ciphers in "-jumbo" versions."

[JohnTheRipper Homepage](https://www.openwall.com/john/)

[JohnTheRipper Github](https://github.com/openwall/john)

### HCXTools

From their github "Small set of tools convert packets from captures (h = hash, c = capture, convert and calculate candidates, x = different hashtypes) for the use with latest hashcat or John the Ripper. The tools are 100% compatible to hashcat and John the Ripper and recommended by hashcat. This branch is pretty closely synced to hashcat git and John the Ripper git."

[HCXTools Github](https://github.com/ZerBea/hcxtools)

## Install

I've installed this on ubuntu with:

`sudo apt-get -y install git build-essential libssl-dev zlib1g-dev yasm pkg-config libgmp-dev libpcap-dev libbz2-dev nvidia-opencl-dev cmake bison flex clang`

`sudo git clone --recursive https://github.com/teeshop/rexgen.git && cd rexgen`

`sudo ./install.sh`

`sudo ldconfig`

`cd /opt/`

`sudo git clone https://github.com/openwall/john -b bleeding-jumbo john`

`cd /opt/john/src`

`sudo ./configure --enable-rexgen && sudo make -s clean && sudo make -sj4`

This will install john and johns other conversion tools to `/opt/john/run/`

### HCXTools

`sudo apt install libcurl4-openssl-dev libssl-dev zlib1g-dev`

`cd /opt/`

`sudo git clone https://github.com/ZerBea/hcxtools.git && cd hcxtools`

`sudo make`

`sudo make install`

## Usage
