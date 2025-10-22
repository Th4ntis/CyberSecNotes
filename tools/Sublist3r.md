# About
Fast subdomains enumeration tool for penetration testers. Sublist3r is a python tool designed to enumerate subdomains of websites using OSINT. It helps penetration testers and bug hunters collect and gather subdomains for the domain they are targeting. Sublist3r enumerates subdomains using many search engines such as Google, Yahoo, Bing, Baidu and Ask. Sublist3r also enumerates subdomains using Netcraft, Virustotal, ThreatCrowd, DNSdumpster and ReverseDNS.
## Links
[Github](https://github.com/aboul3la/Sublist3r)
# Installing
- From source - Recommended in a VENV
```
git clone https://github.com/aboul3la/Sublist3r.git && cd sublist3r
sudo apt-get install python-requests python-dnspython python-argparse
sudo pip install -r requirements.txt
```
# Usage
- Enumerate subdomains and show the results in realtime:
```
python sublist3r.py -v -d example.com
```
- Enumerate subdomains and use specific engines such Google, Yahoo and Virustotal engines
```
python sublist3r.py -e google,yahoo,virustotal -d example.com
```