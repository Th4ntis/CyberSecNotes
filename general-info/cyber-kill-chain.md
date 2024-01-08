# Cyber Kill Chain

## About

The [cyber kill chain](https://www.crowdstrike.com/cybersecurity-101/cyber-kill-chain/) is an adaptation of the military’s kill chain, which is a step-by-step approach that identifies and stops enemy activity. Originally developed by Lockheed Martin in 2011, the cyber kill chain outlines the various stages of several common cyberattacks and, by extension, the points at which the information security team can prevent, detect or intercept attackers.

The cyber kill chain is intended to defend against sophisticated cyberattacks, also known as [advanced persistent threats (APTs)](https://www.crowdstrike.com/cybersecurity-101/advanced-persistent-threat-apt/), wherein attackers spend significant time surveilling and planning an attack. Most commonly these attacks involve a combination of malware, ransomware, Trojans, spoofing and [social engineering techniques](https://www.crowdstrike.com/cybersecurity-101/social-engineering-attacks/) to carry out their plan.

There are other Kill Chains out there, which some can found [here](https://www.sentinelone.com/cybersecurity-101/cyber-kill-chain/) from SentinelOne but here is the standard one. Another good article from Varonis can be found [here](https://www.varonis.com/blog/cyber-kill-chain).

## Standard Kill Chain

The standard kill chain is broken into these phases:

<figure><img src="../.gitbook/assets/image (664).png" alt=""><figcaption></figcaption></figure>

* **Phase 1: Reconnaissance**
* **Phase 2: Weaponization**
* **Phase 3: Delivery**
* **Phase 4: Exploitation**
* **Phase 5: Installation**
* **Phase 6: Command and Control**
* **Phase 7: Actions on Objective**

### **Phase 1: Reconnaissance**

Attackers identify a target and explores vulnerabilities and weaknesses that can be exploited within the network. As part of this process, the attacker may harvest login credentials or gather other information, such as email addresses, user IDs, physical locations, software applications and operating system details, etc. all of which may be useful in phishing or spoofing attacks.

### Phase 2: **Weaponization**

Attackers create an attack vector, such as remote access malware, ransomware, virus or worm that can exploit a known vulnerability. The attacker may also set up back doors so that they can continue to access to a system if their original point of entry is identified and closed by network administrators.

### Phase 3: **Delivery**

The attacker launches the attack. The specific steps taken will depend on the type of attack they intend to carry out. Eg. the attacker may send email attachments or a malicious link to spur user activity to advance the plan. This activity may be combined with social engineering techniques to increase the effectiveness of the campaign.

### Phase 4: **Exploitation**

This phase is pretty simple. The malicious code or file is executed within the target system.

### Phase 5: **Installation**

Following the Exploitation phase, the malware or other attack vector will be installed on the target system. This is a turning point in the attack lifecycle, as the threat actor has entered the system and can now assume control.

### Phase 6: **Command and Control (C2)**

The attacker is able to use the malware to assume remote control of a device or identity within the target network. The attacker may also work to move laterally throughout the network, expanding their access and establishing more points of entry for the future.

### Phase 7: **Actions on Objective**

The attacker takes steps to carry out their intended goals, which may include data theft, destruction, encryption or exfiltration.

\
