# MITRE ATT\&CK

## General

[MITRE ATT\&CK](https://attack.mitre.org/) is a knowledge base of adversary tactics and techniques based on real-world observations. It is a free, giant, organized list of all the known tricks hackers use, so the good guys can recognize them, talk about them, and stop them.

### Analogy

Burglars like to break into houses. Over many years, people watched how burglars do it and wrote every trick down in one giant notebook:

* "Some climb through an unlocked window."
* "Some trick you into opening the door."
* "Some hide in the basement for days before stealing things."
* "Some make copies of your house keys."

MITRE ATT\&CK is that giant notebook, but for computer hackers instead of burglars.

It's a big, free list that organizes all the sneaky tricks hackers use when they attack computers and networks. Each trick has a name and a little card explaining it. The notebook is split into steps of an attack, in the order a hacker usually does them. These are called tactics - they're the why (the goal):

1. Get in (break through the door)
2. Stay in (hide so you can come back)
3. Look around (snoop through rooms)
4. Grab the goodies (steal the stuff)
5. Sneak it out (carry it away without being seen)

Under each goal are the specific techniques. The how, the actual tricks (like "pick the lock" vs. "break the window"). The defenders (the people protecting the computers, like digital security guards) use this notebook to:

* Check their house: "Do we have a lock on this window the burglars like?"
* Speak the same language: instead of describing an attack in a messy way, everyone just says the trick's name, and they all know exactly what happened.
* Practice: good-guy hackers pretend to be the bad guys using tricks from the notebook, to see if the alarms go off.

(The name is a hint too: ATT\&CK stands for Adversarial Tactics, Techniques, and Common Knowledge. "MITRE" is just the name of the non-profit company that keeps the notebook.)

## Resources

* [MITRE ATT\&CK Homepage](https://attack.mitre.org/)
* [MITRE ATT\&CK Navigator](https://mitre-attack.github.io/attack-navigator/)
* [MITRE Engage](https://engage.mitre.org/)
* [MITRE D3FEND](https://d3fend.mitre.org/)
* [MITRE Engenuity](https://mitre-engenuity.org/)
* [ATT\&CK matrix and technique pages](https://attack.mitre.org)
* [Caldera](https://caldera.mitre.org)
* [Atomic Red Team](https://github.com/redcanaryco/atomic-red-team)
* [Center for Threat-Informed Defense](https://mitre-engenuity.org/cybersecurity/center-for-threat-informed-defense)
* [Video overview of the framework.](https://youtu.be/Yxv1suJYMI8)

## How Attackers use it

As an Attacker (Red Team / Pentester), the mindset is: use ATT\&CK to plan, structure, and report an engagement so it mirrors how real adversaries behave.

### Threat emulation / adversary emulation

Pick a real threat group that would realistically target your client (ATT\&CK Groups like G0016 APT29) and copy their known techniques. This makes the test realistic instead of just "throw tools at it." MITRE's Adversary Emulation Plans (part of the CTID / Center for Threat-Informed Defense) give ready-made playbooks.

### Plan the kill chain across tactics

Walk left-to-right through the tactics and pick a technique for each phase you need:

* Initial Access > T1566 Phishing
* Execution > T1059.001 PowerShell
* Persistence > T1547 Boot/Logon Autostart
* Credential Access > T1003 OS Credential Dumping
* Lateral Movement > T1021 Remote Services
* Exfiltration > T1041 Exfil Over C2 Channel

### Pick tooling per technique

Each technique page links the procedures and often the tools used. Frameworks map directly to ATT\&CK:

* Atomic Red Team - small scripted tests, one per technique ID.
* Caldera - MITRE's automated adversary emulation platform.
* Cobalt Strike / Sliver / Metasploit - map their modules to technique IDs.

### Report in ATT\&CK language

Instead of "we got in and moved around," your report says: "Achieved initial access via T1566.001, executed via T1059.001, dumped creds via T1003.001." The defender can act on that immediately because it maps to their detections and the gaps you exposed.

## How Defender use it

As a Defender (Blue Team / SOC) the mindset is: use ATT\&CK to measure coverage, build detections, and prioritize based on what adversaries actually do.

### Detection engineering

For each technique, ask: "Would we see this?" Build a detection and map it to the technique ID. Each ATT\&CK technique page lists:

* Data Sources - what telemetry reveals it (process creation, command-line, authentication logs, network traffic).
* Detection guidance - what the behavior looks like.
* Mitigations - preventive controls (M1049 Antivirus, M1030 Network Segmentation).

Example: for T1059.001 PowerShell, you'd enable PowerShell script-block logging + Module logging and alert on suspicious cmdlets.

### Coverage mapping with the ATT\&CK Navigator

The [ATT\&CK Navigator](https://mitre-attack.github.io/attack-navigator) is a free web tool where you color techniques on the matrix:

* Green = we have a solid detection
* Yellow = partial
* Red = blind spot

This instantly shows your gaps and where to invest next. You can also overlay a specific threat group's techniques to see "are we covered against this adversary?"

### Threat-informed prioritization

You can't defend everything equally. Use Cyber Threat Intelligence to find which groups target your industry, overlay their techniques, and prioritize those. Pair with the "Top ATT\&CK Techniques" methodology to focus on the highest-value detections.

### Purple teaming (closing the loop)

This is where both sides meet: Red runs a technique (e.g. via Atomic Red Team), Blue checks whether their tooling alerted. If no alert fired > that's a detection gap > build the rule > re-test. The ATT\&CK ID is the common key tying the attack action to the detection.

### Mapping tools to the framework

* Sigma rules - detection rules tagged with ATT\&CK IDs.
* SIEM dashboards (Splunk, Elastic) - alerts tagged by technique for coverage tracking.
* EDR (CrowdStrike, Defender, SentinelOne) - map alerts to ATT\&CK natively.
* [ATT\&CK Navigator](https://mitre-attack.github.io/attack-navigator) - formally score data-source and detection coverage.
