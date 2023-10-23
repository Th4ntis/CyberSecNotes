# Shodan

## About

[Shodan.io](https://www.shodan.io/) is a search engine for the Internet of Things. Shodan scans the whole internet and indexes the services run on each IP address.&#x20;

## Usage

### General

Let's say we want to find specific information on a website or IP, we an input the IP into the search and find what services are running and what ports are open. Some larger companies have proxies between their server and the internet so we may need to get the actual IPs using Autonomous System Numbers.

### Autonomous System Numbers

An autonomous system number (ASN) is a global identifier of a range of IP addresses. If you are an enormous company like Google you will likely have your own ASN for all of the IP addresses you own. We can put the IP address into an ASN lookup tool such as [ASNLookup](http://asnlookup.com/lookup), Which tells us they have the ASN AS14061.

### Banners

To get the most out of Shodan, it’s important to understand the search query syntax. Devices run services, and Shodan stores information about them. The information is stored in a banner. It’s the most fundamental part of Shodan.

### Filters

On the Shodan.io homepage, we can click on “[explore](https://www.shodan.io/explore)” to view the most up voted search queries. The most popular one is webcams.&#x20;

**Note: this is a grey area. It is legal to view a publicly accessible webcam, it is illegal to try to break into a password protected one. Use your brain and research the laws of your country!**&#x20;

One of the other most up voted searches is a search for [MYSQL databases](https://www.shodan.io/search?query=product%3AMySQL). If we look at the search, we can see it is another filter, _product:MySQL_.

Shodan has many powerful filters. One is the vuln filter, which let’s us search for IP addresses vulnerable to an exploit. Let’s say we want to find IP addresses vulnerable to Eternal Blue: _vuln:ms17-010_, however, this is only available for academic or business users, to prevent bad actors from abusing this!

City Country Geo (coordinates) Hostname net (based on IP / CIDR) OS (find operating systems) port before/after (timeframes)

**PS:** You can automatically filter on Shodan by clicking the things in the left hand side bar!

### Shodan Monitoring

Shodan Monitor is an application for monitoring your devices in your own network. In their words, "Keep track of the devices that you have exposed to the Internet. Setup notifications, launch scans and gain complete visibility into what you have connected".&#x20;

Previously we had to do this using their API, but now we have this fancy application. Access the dashboard via [this link](https://monitor.shodan.io/dashboard). You’ll see it’s asking for an IP range. Once we add a network, we can see it in our dashboard. If we click on the settings cog, we can see that we have a range of “scans” Shodan performs against our network. Anytime Shodan detects a security vulnerability in one of these categories, it will email us. If we go to the dashboard again we can see it lays some things out for us. Most notably:

* Top Open Ports (most common)
* Top Vulnerabilities (stuff we need to deal with right away)
* Notable Ports (unusual ports that are open)
* Potential Vulenrabilites
* Notable IPs (things we should investigate in more depth). The interesting part is that you can actually monitor other peoples networks using this. For bug bounties you can save a list of IPs and Shodan will email you if it finds any problems.

### Shodan Dorking

Shodan has some lovely webpages with Dorks that allow us to find things. Their search example webpages feature some. Some fun ones include: `has_screenshot:true encrypted attention` Which uses optical character recognition and remote desktop to find machines compromised by ransomware on the internet. `screenshot.label:ics` `vuln:CVE-2014-0160` Internet connected machines vulenrable to heartbleed. Note: CVE search is only allowed to academic or business subscribers. Solar Winds Supply Chain Attack by using Favicons: `http.favicon.hash:-1776962843`

### Shodan Extention

Shodan also has an [extension](https://chrome.google.com/webstore/detail/shodan/jjalcfnidlmpjhdfepjhjbhnhkbgleap). When installed, you can click on it and it’ll tell you the IP address of the webserver running, what ports are open, where it’s based and if it has any security issues. I imagine this is a good extension for any people interested in bug bounties, being quickly able to tell if a system looks vulnerable or not based on the Shodan output.

### Exploring API

Shodan.io has an API! It requires an account, so I won't talk about it here. If you want to explore the Shodan API, I've written a blog post about finding Pi-Holes with it [here](https://github.com/beesecurity/How-I-Hacked-Your-Pi-Hole/blob/master/README.md). The API lets us programmatically search Shodan and receive a list of IP addresses in return. If we are a company, we can write a script to check over our IP addresses to see if any of them are vulnerable.

PS: You can automatically filter on Shodan by clicking the things in the left hand side bar!
