# About

[Metasploit](https://www.metasploit.com/) is a very popular and useful exploitation framework. It's an industry standard that can be used for scanning, exploitation and more. Maintained by [Rapid 7](https://www.rapid7.com/), it is a collection of not only thoroughly tested exploits but also auxiliary and post-exploitation tools.
## Links
[Metasploit Documentation](https://docs.metasploit.com/)
[Metasploit Unleashed](https://www.offensive-security.com/metasploit-unleashed/)
[Metasploit Github](https://github.com/rapid7/metasploit-framework)
[Using Metasploit](https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html)
# Installing
[Per their documentation](https://docs.metasploit.com/docs/using-metasploit/getting-started/nightly-installers.html), we can install it on MacOS and Linux with:

```
curl https://raw.githubusercontent.com/rapid7/metasploit-omnibus/master/config/templates/metasploit-framework-wrappers/msfupdate.erb > msfinstall && \
  chmod 755 msfinstall && \
  ./msfinstall
```

We can also [install it on on Windows](https://docs.metasploit.com/docs/using-metasploit/getting-started/nightly-installers.html#installing-metasploit-on-windows) from [their installer](https://windows.metasploit.com/metasploitframework-latest.msi).
# Usage
Metasploit can do various things. Start it with `msfconsole`. The banner will change almost every time you start it, but we can remove the banner with `msfconsole -q`. We can also initialize a database with `msfdb init`. The console can be used just like a regular command-line shellwhere we can run commands such as `ls`, `mkdir`, or `ping`.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FNKMBbey8QICZLEwKu3gE%252Fimage.png%3Falt%3Dmedia%26token%3Dc7653261-3504-4a76-a700-f7267a95d895&width=768&dpr=4&quality=100&sign=a2e4b730&sv=2)

Once in, run `help` get a list of commands. A very helpful one is `search` that we can use to search the available modules with what they are used for. Other commands include `use`, `set`, `options`.The `use` command select which payload we want to us. The `set` command sets options for the used payload. `Options` shows options that are required such as local host, remote host, if we want to provide credentials, etc.
## Searching
Running just `search` alone can provide a helpful list of keywords to use when searching. But for example I will search for portscan modules.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F2z1QBkxkhLLAe3ExYCMQ%252Fimage.png%3Falt%3Dmedia%26token%3D9bf1402c-eae6-4034-b770-41e694dae1b6&width=768&dpr=4&quality=100&sign=4707927d&sv=2)

We see the Number of the module, the name, and other information on what it's used for. The number is helpful to use instead of the full name but either can be used. When you find a module you want to use or look at, you use the `use` command with the name OR the number.

Eg. `use 5` will select the `auxiliary/scanner/portscan/tcp` module and we sill see our payload selected.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FaMps3tsZ5OmMMkzADZmh%252Fimage.png%3Falt%3Dmedia%26token%3D22b05d98-61d4-4152-bf56-05b951f9b151&width=768&dpr=4&quality=100&sign=20be26ad&sv=2)
## Options
Running `options` once we have our payload selected will show us a list of options for the payload and will tell us if they are required or not.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FuCsUZllIuXhZO7Hr3sUg%252Fimage.png%3Falt%3Dmedia%26token%3Dfca015a7-4f43-4d88-b16f-4de4ff09fc39&width=768&dpr=4&quality=100&sign=f2843e23&sv=2)

we can set the options with `set`, I will set the remote host (`RHOSTS`) as that is required but does not have a current setting. Eg. `set rhosts 192.168.50.55`

Running options again will show us our set options, then we can type `run` or `exploit` to run the payload.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FdrC8y2uGhrb4XCjplCEu%252Fimage.png%3Falt%3Dmedia%26token%3D57bde8b2-a5d3-47b4-a981-323ed5d425c6&width=768&dpr=4&quality=100&sign=864f2c62&sv=2)
# Database
You will first need to start the PostgreSQL database: `systemctl start postgresql`. Then you will need to initialize the Metasploit Database using `msfdb init`. Once in the console, verify connectivity with `db_status`.

```
msfconsole -q                                                                                                                                                                                 ✔  12s  
dbmsf6 > db_status
[*] Connected to msf. Connection type: postgresql.
```

You can create workspaces to isolate different projects. When first launched, you should be in the default workspace. You can list available workspaces running `workspace`. You can add a workspace using the `-a` parameter or delete a workspace using the `-d` parameter. Change databases with `workspace (workspace name)`.

```
msf6 > workspace
  demo
* default
msf6 > workspace demo
[*] Workspace: demo
msf6 > workspace 
  default
* demo
msf6 >
```
## Scanning
We can do nmap scans within the console as well and store the results into a database or use modules, like shown above.

If you run a Nmap scan using the `db_nmap` shown below, all results will be saved to the database.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FYOiBoHTN753zZHLGr3sb%252Fimage.png%3Falt%3Dmedia%26token%3Da17d3e20-0eed-40b1-80df-525521b78952&width=768&dpr=4&quality=100&sign=8c82afff&sv=2)

The information relevant to hosts and services running on target systems with the `hosts` and `services` commands. Once the host information is stored in the database, you can use the `hosts -R` command to add this value to the RHOSTS parameter.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FUnCRW9d5wmMRCeYdF4Fz%252Fimage.png%3Falt%3Dmedia%26token%3D47ac9713-58d4-448c-9e79-43359429d76b&width=768&dpr=4&quality=100&sign=5a9dcf66&sv=2)

The services command used with the `-S` parameter will allow you to search for specific services in the environment.
# Payloads and Sessions/Shells
Most of the exploits will have a preset default payload. But running `show payloads` will list other commands you can use with that specific exploit. You can run `set payload` to make your choice. **Note:** that choosing a working payload could become a trial and error process due to environmental or OS restrictions such as firewall rules, anti-virus, file writing, or the program performing the payload execution isn't available.

Once a session is opened, you can background it using `CTRL+Z` or abort it using `CTRL+C`. Backgrounding a session will be useful when working on more than one target simultaneously or on the same target with a different exploit and/or shell. The `sessions` command will list all active sessions and supports a number of options that will help you manage sessions better. You can interact with any existing session using the `sessions -i` command followed by the session ID (`sessions -i 1`).

