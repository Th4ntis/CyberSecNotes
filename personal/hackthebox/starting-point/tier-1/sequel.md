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

```bash
mysql --help | grep user    
  -u, --user=name     User for login if not current user.
user                                      (No default value)
```

Answer: **-u**

## Task 5

#### Which username allows us to log into MariaDB without providing a password?

Google'd for this answer

> Using unix\_socket means that if you are the system root user, you can login as root@locahost without a password. This technique was pioneered by Otto Kekäläinen in Debian MariaDB packages and has been successfully used in Debian since as early as MariaDB 10.0.

Answer: **root**

## Task 6

#### What symbol can we use to specify within the query that we want to display everything inside a table?

The typical common symbol that's used mean "everything", the asterisk/wildcard.

Answer: **\***

## Task 7

#### What symbol do we need to end each query with?

Looking at SQL examples, we see queries ending with a semi-colon (;)

```sql
use users_database;
```

Answer: **;**

## Task 8

#### Submit root flag

```sql
/mysql -h 10.129.19.38 -u root
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 132
Server version: 5.5.5-10.3.27-MariaDB-0+deb10u1 Debian 10

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| htb                |
| information_schema |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.05 sec)

mysql> use htb;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
mysql> show tables;
+---------------+
| Tables_in_htb |
+---------------+
| config        |
| users         |
+---------------+
2 rows in set (0.05 sec)

mysql> select * from config;
+----+-----------------------+----------------------------------+
| id | name                  | value                            |
+----+-----------------------+----------------------------------+
|  1 | timeout               | 60s                              |
|  2 | security              | default                          |
|  3 | auto_logon            | false                            |
|  4 | max_size              | 2M                               |
|  5 | flag                  | 7b4bec00d1a39e3dd4e021ec3d915da8 |
|  6 | enable_uploads        | false                            |
|  7 | authentication_method | radius                           |
+----+-----------------------+----------------------------------+
7 rows in set (0.05 sec)

mysql>
```

Answer: 7b4bec00d1a39e3dd4e021ec3d915da8

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

X Answer: **XXX**

## Task 3

#### What community-developed MySQL version is the target running?

X Answer: **XXX**

## Task 4

#### What switch do we need to use in order to specify a login username for the MySQL service?

X Answer: **XXX**

## Task 5

#### Which username allows us to log into MariaDB without providing a password?

X Answer: **XXX**

## Task 6

#### What symbol can we use to specify within the query that we want to display everything inside a table?

X Answer: **XXX**

## Task 7

#### What symbol do we need to end each query with?

X Answer: **XXX**

## Task 8

#### Submit root flag

X Answer: **XXX**
