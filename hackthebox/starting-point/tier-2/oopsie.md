# Oopsie

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.95.191 -oA Oopsie
```

<figure><img src="../../../.gitbook/assets/image (898).png" alt=""><figcaption></figcaption></figure>

## Task 1

With what kind of tool can intercept web traffic?

<figure><img src="../../../.gitbook/assets/image (899).png" alt=""><figcaption></figcaption></figure>

Answer: Proxy

## Task 2

What is the path to the directory on the webserver that returns a login page?  Answer: /cdn-cgi/login

## Task 3

What can be modified in Firefox to get access to the upload page?

Answer: Cookie

## Task 4

What is the access ID of the admin user?

<figure><img src="../../../.gitbook/assets/image (900).png" alt=""><figcaption></figcaption></figure>

Answer: 34322

## Task 5

On uploading a file, what directory does that file appear in on the server?

<figure><img src="../../../.gitbook/assets/image (901).png" alt=""><figcaption></figcaption></figure>

Answer: /uploads/

## Task 6

What is the file that contains the password that is shared with the robert user?

<figure><img src="../../../.gitbook/assets/image (902).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (903).png" alt=""><figcaption></figcaption></figure>

Upgrade to a functional shell:

```bash
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

&#x20;

<figure><img src="../../../.gitbook/assets/image (904).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (905).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (906).png" alt=""><figcaption></figcaption></figure>

Answer: db.php

## Task 7

What executible is run with the option "-group bugtracker" to identify all files owned by the bugtracker group?

<figure><img src="../../../.gitbook/assets/image (907).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (908).png" alt=""><figcaption></figcaption></figure>

Answer: find

## Task 8

Regardless of which user starts running the bugtracker executable, what's user privileges will use to run?

<figure><img src="../../../.gitbook/assets/image (909).png" alt=""><figcaption></figcaption></figure>

Answer: root

## Task 9

What SUID stands for?

Answer: Set owner User ID

## Task 10

What is the name of the executable being called in an insecure manner?

<figure><img src="../../../.gitbook/assets/image (910).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (911).png" alt=""><figcaption></figcaption></figure>

Answer: cat

## Task 11

Submit User Flag

<figure><img src="../../../.gitbook/assets/image (912).png" alt=""><figcaption></figcaption></figure>

Answer: f2c74ee8db7983851ab2a96a44eb7981

## Task 12

Submit Root Flag

<figure><img src="../../../.gitbook/assets/image (913).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (914).png" alt=""><figcaption></figcaption></figure>

Answer: af13b0bee69f8a877c3faf667f7beacf
