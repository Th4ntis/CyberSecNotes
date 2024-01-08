# Mongod

## Initial Scan

```
sudo nmap -p- -sT -sV -T4 -v 10.129.183.59
Starting Nmap 7.80 ( https://nmap.org ) at 2022-11-04 23:11 EDT
NSE: Loaded 45 scripts for scanning.
Initiating Ping Scan at 23:11
Scanning 10.129.183.59 [4 ports]
Completed Ping Scan at 23:11, 0.08s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 23:11
Completed Parallel DNS resolution of 1 host. at 23:11, 0.09s elapsed
Initiating Connect Scan at 23:11
Scanning 10.129.183.59 [65535 ports]
Discovered open port 22/tcp on 10.129.183.59
Discovered open port 27017/tcp on 10.129.183.59
Completed Connect Scan at 23:11, 19.21s elapsed (65535 total ports)
Initiating Service scan at 23:11
Scanning 2 services on 10.129.183.59
Completed Service scan at 23:12, 6.11s elapsed (2 services on 1 host)
NSE: Script scanning 10.129.183.59.
Initiating NSE at 23:12
Completed NSE at 23:12, 0.01s elapsed
Initiating NSE at 23:12
Completed NSE at 23:12, 0.00s elapsed
Nmap scan report for 10.129.183.59
Host is up (0.053s latency).
Not shown: 65533 closed ports
PORT      STATE SERVICE VERSION
22/tcp    open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.5 (Ubuntu Linux; protocol 2.0)
27017/tcp open  mongodb MongoDB 3.6.8
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 25.99 seconds
           Raw packets sent: 4 (152B) | Rcvd: 1 (28B)
```

## Task 1

**How many TCP ports are open on the machine?**

Found from the initial scan

Answer: 2

## Task 2

**Which service is running on port 27017 of the remote host?**

Found from the initial scan

Answer: MongoDB 3.6.8

## Task 3

**What type of database is MongoDB? (Choose: SQL or NoSQL)**

As they only give us 2 options and it's more than 3 characters long, BUT also a google search will show: "MongoDB is a source-available cross-platform document-oriented database program. Classified as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas."

Answer: NoSQL

## Task 4

**What is the command name for the Mongo shell that is installed with the mongodb-clients package?**

Google search and looking on their webpage reveal: "The `mongo` shell is included as part of the MongoDB server installation. If you have already installed the server, the `mongo` shell is installed to the same location as the server binary."

With this, lets connect to the mongo databse on the target machine

<figure><img src="../../../.gitbook/assets/image (535).png" alt=""><figcaption></figcaption></figure>

Answer: mongo

## Task 5

**What is the command used for listing all the databases present on the MongoDB server? (No need to include a trailing ;)**

Another google search.

<figure><img src="../../../.gitbook/assets/image (239).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (260).png" alt=""><figcaption></figcaption></figure>

Answer: show dbs

## Task 6

**What is the command used for listing out the collections in a database? (No need to include a trailing ;)**

Similar to last answer just with collections rather than databases.

We see the secsitive\_information database, so let use that.

<figure><img src="../../../.gitbook/assets/image (244).png" alt=""><figcaption></figcaption></figure>

Answer: show collections

## Task 7

**What is the command used for dumping the content of all the documents within the collection named flag in a format that is easy to read?**

Googling around says "Using the db.collection.find() command." So we know our collection is called flag, use the collection name flag instead of the word collection.

<figure><img src="../../../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

But this doesn't give us the full answer. After more googling around I found [this blog post](https://roytuts.com/how-to-make-output-mongodb-find-readable-in-shell/) mentioning the pretty() function.

<figure><img src="../../../.gitbook/assets/image (180).png" alt=""><figcaption></figcaption></figure>

Answer: db.flag.find().pretty()



## Task 8

**Submit the root flag**

From previous command/task

Answer: 1b6e6fb359e7c40241b6d431427ba6ea
