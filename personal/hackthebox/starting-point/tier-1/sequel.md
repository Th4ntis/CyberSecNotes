# Sequel

## Initial Scan

```bash
nmap -sT -sV -T4 -A -v 10.129.19.38 
Starting Nmap 7.80 ( https://nmap.org ) at 2022-08-10 17:15 EDT
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 17:15
Completed NSE at 17:15, 0.00s elapsed
Initiating NSE at 17:15
Completed NSE at 17:15, 0.00s elapsed
Initiating NSE at 17:15
Completed NSE at 17:15, 0.00s elapsed
Initiating Ping Scan at 17:15
Scanning 10.129.19.38 [2 ports]
Completed Ping Scan at 17:15, 0.05s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 17:15
Completed Parallel DNS resolution of 1 host. at 17:15, 0.08s elapsed
Initiating Connect Scan at 17:15
Scanning 10.129.19.38 [1000 ports]
Discovered open port 3306/tcp on 10.129.19.38
Completed Connect Scan at 17:15, 0.81s elapsed (1000 total ports)
Initiating Service scan at 17:15
Scanning 1 service on 10.129.19.38
Completed Service scan at 17:17, 157.53s elapsed (1 service on 1 host)
NSE: Script scanning 10.129.19.38.
Initiating NSE at 17:17
Completed NSE at 17:18, 20.11s elapsed
Initiating NSE at 17:18
Completed NSE at 17:18, 1.06s elapsed
Initiating NSE at 17:18
Completed NSE at 17:18, 0.00s elapsed
Nmap scan report for 10.129.19.38
Host is up (0.052s latency).
Not shown: 999 closed ports
PORT     STATE SERVICE VERSION
3306/tcp open  mysql?
| mysql-info: 
|   Protocol: 10
|   Version: 5.5.5-10.3.27-MariaDB-0+deb10u1
|   Thread ID: 128
|   Capabilities flags: 63486
|   Some Capabilities: Support41Auth, Speaks41ProtocolOld, Speaks41ProtocolNew, LongColumnFlag, IgnoreSigpipes, SupportsLoadDataLocal, DontAllowDatabaseTableColumn, SupportsTransactions, ConnectWithDatabase, SupportsCompression, InteractiveClient, IgnoreSpaceBeforeParenthesis, FoundRows, ODBCClient, SupportsAuthPlugins, SupportsMultipleResults, SupportsMultipleStatments
|   Status: Autocommit
|   Salt: aNCEn{?ipx-pp`q6W7KS
|_  Auth Plugin Name: mysql_native_password

NSE: Script Post-scanning.
Initiating NSE at 17:18
Completed NSE at 17:18, 0.00s elapsed
Initiating NSE at 17:18
Completed NSE at 17:18, 0.00s elapsed
Initiating NSE at 17:18
Completed NSE at 17:18, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 179.92 seconds
```

## Task 1

#### What does the acronym SQL stand for?

Previous rooms and general knowledge

Answer: **Structured Query Language**

## Task 2

#### During our scan, which port running mysql do we find?

Found in initial scan

Answer: **3306**

## Task 3

#### What community-developed MySQL version is the target running?

Found in initial scan

Answer: MariaDB

## Task 4

#### What switch do we need to use in order to specify a login username for the MySQL service?

`mysql --help`



Answer: **-u**

## Task 5

#### Which username allows us to log into MariaDB without providing a password?



Answer: **XXX**

## Task 6

#### What symbol can we use to specify within the query that we want to display everything inside a table?



Answer: **XXX**

## Task 7

#### What symbol do we need to end each query with?



Answer: **XXX**

## Task 8

#### Submit root flag



Answer: **XXX**
