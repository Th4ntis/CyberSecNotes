# Bike

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.245.220 -oA Bike
```

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

## Task 1

What TCP ports does nmap identify as open? Answer with a list of ports seperated by commas with no spaces, from low to high. - Found in the initial Scan

Answer: 22,80

## Task 2

What software is running the service listening on the http/web port identified in the first question? - Also found in the initial scan

Answer: Node.js

## Task 3

What is the name of the Web Framework according to [Wappalyzer](https://www.wappalyzer.com/)? - Using Wappalyzer we can see.&#x20;

<figure><img src="../../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

Answer: Express

## Task 4

What is the name of the vulnerability we test for by submitting \{{7\*7\}}? - Node.js servers often use a software called a Template Engine. Looking into vulnerabilities we see a common one.

Answer: Server side template injection

## Task 5

What is the templating engine being used within Node.JS?

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Answer: Handlebars

## Task 6

What is the name of the BurpSuite tab used to encode text?

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

Answer: Decoder

## Task 7

In order to send special characters in our payload in an HTTP request, we'll encode the payload. What type of encoding do we use?

Answer: URL

## Task 8

When we use [a payload from HackTricks](https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection#handlebars-nodejs) to try to run system commands, we get an error back. What is "not defined" in the response error?

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

Answer: require

## Task 9

What variable is the name of the top-level scope in Node.JS?

Answer: Global

## Task 10

By exploiting this vulnerability, we get command execution as the user that the webserver is running as. What is the name of that user?

<figure><img src="../../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

Answer: root

## Task 11

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

Answer: 6b258d726d287462d60c103d0142a81c
