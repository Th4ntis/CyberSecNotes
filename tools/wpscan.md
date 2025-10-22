# WPScan

## About

WPScan WordPress security scanner. Written for security professionals and blog maintainers to test the security of their WordPress websites. The WPScan CLI tool uses the [WordPress Vulnerability Database API](https://wpscan.com/api) to retrieve WordPress vulnerability data in real time. Usage of this tool does require an API, which can be done by registering an account [here](https://wpscan.com/register).

### Links

[Homepage](https://wpscan.com/)

[Github](https://github.com/wpscanteam/wpscan)

[WPScan Register for an API](https://wpscan.com/register)

## Usage

### Key

* vp = virtual plugins
* u = usernames
* vt = virtual themes
* tt = timtums
* General Use

```
wpscan --url [URL] --api-token [TOKEN] --enumerate vp,u,vt,tt --random-user-agent
```
