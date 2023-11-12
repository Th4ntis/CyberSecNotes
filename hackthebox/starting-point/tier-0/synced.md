# Synced

## Initial Scan

```
sudo nmap -T4 -Pn -sV -sC -v 10.129.243.254 -oA Synced
```

<figure><img src="../../../.gitbook/assets/image (15) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Task 1

What is the default port for rsync? - This is found in the initial scan, OR a google search will tell you. Answer: 873

## Task 2

How many TCP ports are open on the remote host? - Also found from the initial scan Answer: 1

## Task 3

What is the protocol version used by rsync on the remote machine? - Also found from the initial scan Answer: 31

## Task 4

What is the most common command name on Linux to interact with rsync? - rsync is also a command Answer: rsync

## Task 5

What credentials do you have to pass to rsync in order to use anonymous authentication? Answer: None

## Task 6

What is the option to only list shares and files on rsync? - Look at `rsync -h`  Answer: list-only

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Task 7

Get the flag

<figure><img src="../../../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Sync the file, cat it. Flag obtained `rsync 10.129.243.254::public/flag.txt flag.txt`

<figure><img src="../../../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Answer: 72eaf5344ebb84908ae543a719830519
