# Cyber Kill Chain

## About

The [Cyber Kill Chain](https://www.crowdstrike.com/cybersecurity-101/cyber-kill-chain/) is an adaptation of the military's kill chain, a step-by-step approach that identifies and stops enemy activity. Originally developed by Lockheed Martin in 2011, the Cyber Kill Chain outlines the various stages of several common cyberattacks and, by extension, the points at which the information security team can prevent, detect, or intercept attackers.

The Cyber Kill Chain is intended to defend against sophisticated cyberattacks, also known as [advanced persistent threats (APTs)](https://www.crowdstrike.com/cybersecurity-101/advanced-persistent-threat-apt/), wherein attackers spend significant time surveilling and planning an attack. Most commonly these attacks involve a combination of malware, ransomware, Trojans, spoofing, and [social engineering techniques](https://www.crowdstrike.com/cybersecurity-101/social-engineering-attacks/) to carry out their plan.

The Cyber Kill Chain can be viewed as a story. It tells you the 7 big chapters of an attack, start to finish, in order. It's simple and great for explaining the "shape" of an attack.

it differs from the [MITRE ATT\&CK](mitre-att-and-ck.md) framework as the MITRE ATT\&CK is an encyclopedia. It's a giant, detailed catalog of the specific tricks attackers actually use at each stage, based on real-world observations.

There are other kill chains out there, some of which can be found [here](https://www.sentinelone.com/cybersecurity-101/cyber-kill-chain/) from SentinelOne, but here is the standard one. Another good article from Varonis can be found [here](https://www.varonis.com/blog/cyber-kill-chain).

## Standard Kill Chain

The standard kill chain is broken into these phases:

<figure><img src="../../.gitbook/assets/image (664).png" alt=""><figcaption></figcaption></figure>

1. **Reconnaissance**
2. **Weaponization**
3. **Delivery**
4. **Exploitation**
5. **Installation**
6. **Command and Control (C2)**
7. **Actions on Objective**

I will add the analogy of a burglar wanting to steal cookies from someone's house, to each of each of the phases.

### Phase 1: Reconnaissance

Attackers identify a target and explore vulnerabilities and weaknesses that can be exploited within the network. As part of this process, the attacker may harvest login credentials or gather other information, such as email addresses, user IDs, physical locations, software applications, and operating system details - all of which may be useful in phishing or spoofing attacks.

Analogy: The thief watches the house. When do people leave? Which window is unlocked? (A hacker looks up info about you - your email, what software you use.)

### Phase 2: Weaponization

Attackers create an attack vector, such as remote access malware, ransomware, a virus, or a worm that can exploit a known vulnerability. The attacker may also set up back doors so that they can continue to access a system if their original point of entry is identified and closed by network administrators.

Analogy: The thief builds a special ladder to reach the window. (A hacker builds a nasty computer bug - "malware" - to sneak in.)

### Phase 3: Delivery

The attacker launches the attack. The specific steps taken depend on the type of attack they intend to carry out. For example, the attacker may send email attachments or a malicious link to spur user activity and advance the plan. This activity may be combined with social engineering techniques to increase the effectiveness of the campaign.

Analogy: The thief carries the ladder over. (A hacker sends you a tricky email with a bad link or attachment.)

### Phase 4: Exploitation

This phase is pretty simple: the malicious code or file is executed within the target system.

Analogy: The thief leans the ladder on the window and climbs. (You click the bad link, and the bug starts working.)

### Phase 5: Installation

Following the exploitation phase, the malware or other attack vector is installed on the target system. This is a turning point in the attack lifecycle, as the threat actor has entered the system and can now assume control.

Analogy: The thief props the door open so they can come back anytime. (The hacker installs their software so they can stay inside your computer.)

### Phase 6: Command and Control (C2)

The attacker is able to use the malware to assume remote control of a device or identity within the target network. The attacker may also work to move laterally throughout the network, expanding their access and establishing more points of entry for the future.

Analogy: The thief calls their boss to ask, "What should I grab?" (The hacker's software secretly talks to the hacker to take orders.)

### Phase 7: Actions on Objective

The attacker takes steps to carry out their intended goals, which may include data theft, destruction, encryption, or exfiltration.

Analogy: Finally, the thief grabs the cookies and runs. (The hacker steals your data, passwords, or money - whatever they came for.)

## How Offense (Red Team / attackers) uses this

* A checklist / game plan - they walk the Kill Chain to make sure they've thought through every stage of a realistic attack.
* Reporting - "We got stopped at Delivery because the email filter caught us, but once in, nobody noticed Installation." That tells the company exactly where it's weak.
* With [ATT\&CK](mitre-att-and-ck.md) - they pick specific real-world techniques to emulate a particular known hacker group ("let's attack like Group X does").

## How Defense (Blue Team / defenders) use this

* Build defenses at every link - the goal is to break the chain as early as possible. A lock for the window, an alarm for the door, a guard for the cookie jar. The earlier you stop the attacker, the less damage.
* Find the gaps - "We're great at catching Delivery (bad emails), but we can't see Command and Control traffic at all." Now they know what to fix.
* Investigate attacks - when something bad happens, they map what they saw onto the stages to figure out how far the attacker got and what to do next.
* With [ATT\&CK](mitre-att-and-ck.md) - they check their detection coverage against the full catalog of techniques ("Can we spot each of these 300 tricks? Which are we blind to?").

