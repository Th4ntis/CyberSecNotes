# About
[Cobalt Strike](https://www.cobaltstrike.com/) is a "**threat emulation software**. Execute targeted attacks against modern enterprises with one of the most powerful network attack kits available to penetration testers. This is **not** compliance testing. Cobalt Strike gives you a post-exploitation agent and covert channels to emulate a quiet long-term embedded actor in your customer’s network. [Malleable C2](https://www.cobaltstrike.com/blog/user-defined-storage-based-covert-communication/) lets you change your network indicators to look like different malware each time. These tools complement Cobalt Strike’s solid social engineering process, its robust collaboration capability, and [unique reports](https://www.cobaltstrike.com/blog/rethinking-reporting-for-red-team-operations/) designed to aid blue team training."

They have a [Community Kit](https://cobalt-strike.github.io/community_kit/) which is a "central repository of extensions written by the user community to extend the capabilities of Cobalt Strike"

Cobalt Strike on [ATT&CK Mitre](https://attack.mitre.org/software/S0154/).
# Attack Package
Cobalt Strike offers a variety of attack packages to conduct a web drive-by attack or to transform an innocent file into a [trojan horse](https://www.makeuseof.com/what-is-a-remote-access-trojan/) for a simulation attack.

Various attack packages offered by Cobalt Strike:
- [Java Applet Attacks](https://www.cobaltstrike.com/help-java-signed-applet-attack)
- [Microsoft Office Documents](https://www.cobaltstrike.com/help-office-macro-attack)
- [Microsoft Windows Programs](https://www.cobaltstrike.com/help-staged-exe)
- [Website Clone Tool](https://www.cobaltstrike.com/help-website-clone-tool)
# Browser Pivoting
Browser Pivoting is a technique that leverages an exploited system to gain access to the browser’s authenticated sessions. It is a powerful way to demonstrate risk with a targeted attack.

Cobalt Strike implements browser pivoting with a proxy server that injects into 32-bit and 64-bit Internet Explorer. When you browse through this proxy server, you inherit cookies, authenticated HTTP sessions, and client SSL certificates.
# Spear Phishing
A variant of phishing, spear phishing is a method that targets specific individuals within an organization. This helps in identifying weak targets within an organization, such as employees that are more prone to security attacks.

Cobalt Strike offers a spear-phishing tool that lets you import a message by replacing links and text to build a convincing phish for you. It allows you to send this pixel-perfect spear-phishing message using an arbitrary message as a template.
# Reporting and Logging
Cobalt Strike also offers post-exploitation reports that provide a timeline and the indicators of compromise detected during red team activity.

Cobalt Strike exports these reports as both PDF and MS Word documents.