# Appointment

## Initial Scan

```bash
nmap -p- -sV -sT -A -v 10.129.17.152
Starting Nmap 7.80 ( https://nmap.org ) at 2022-08-08 20:11 EDT
NSE: Loaded 151 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 20:11
Completed NSE at 20:11, 0.00s elapsed
Initiating NSE at 20:11
Completed NSE at 20:11, 0.00s elapsed
Initiating NSE at 20:11
Completed NSE at 20:11, 0.00s elapsed
Initiating Ping Scan at 20:11
Scanning 10.129.17.152 [2 ports]
Completed Ping Scan at 20:11, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:11
Completed Parallel DNS resolution of 1 host. at 20:11, 0.08s elapsed
Initiating Connect Scan at 20:11
Scanning 10.129.17.152 [65535 ports]
Discovered open port 80/tcp on 10.129.17.152
Connect Scan Timing: About 9.82% done; ETC: 20:16 (0:04:45 remaining)
Connect Scan Timing: About 21.10% done; ETC: 20:16 (0:03:48 remaining)
Connect Scan Timing: About 31.33% done; ETC: 20:16 (0:03:19 remaining)
Connect Scan Timing: About 40.79% done; ETC: 20:16 (0:02:56 remaining)
Connect Scan Timing: About 49.70% done; ETC: 20:16 (0:02:33 remaining)
Connect Scan Timing: About 58.88% done; ETC: 20:16 (0:02:06 remaining)
Connect Scan Timing: About 68.19% done; ETC: 20:16 (0:01:38 remaining)
Connect Scan Timing: About 77.88% done; ETC: 20:16 (0:01:08 remaining)
Connect Scan Timing: About 87.95% done; ETC: 20:16 (0:00:37 remaining)
Completed Connect Scan at 20:16, 310.50s elapsed (65535 total ports)
Initiating Service scan at 20:16
Scanning 1 service on 10.129.17.152
Completed Service scan at 20:16, 6.16s elapsed (1 service on 1 host)
NSE: Script scanning 10.129.17.152.
Initiating NSE at 20:16
Completed NSE at 20:16, 1.52s elapsed
Initiating NSE at 20:16
Completed NSE at 20:16, 0.26s elapsed
Initiating NSE at 20:16
Completed NSE at 20:16, 0.00s elapsed
Nmap scan report for 10.129.17.152
Host is up (0.045s latency).
Not shown: 65534 closed ports
PORT   STATE SERVICE VERSION
80/tcp open  http    Apache httpd 2.4.38 ((Debian))
|_http-favicon: Unknown favicon MD5: 7D4140C76BF7648531683BFA4F7F8C22
| http-methods: 
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Login

NSE: Script Post-scanning.
Initiating NSE at 20:16
Completed NSE at 20:16, 0.00s elapsed
Initiating NSE at 20:16
Completed NSE at 20:16, 0.00s elapsed
Initiating NSE at 20:16
Completed NSE at 20:16, 0.00s elapsed
Read data files from: /usr/bin/../share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 318.94 seconds
```

## Task 1

#### What does the acronym SQL stand for?

Answer: **Structured Query Language**

## Task 2

#### What is one of the most common type of SQL vulnerabilities?

Answer: **SQL Injection**

## Task 3

#### What does PII stand for?

Answer: **Personally Identifiable Information**

## Task 4

#### What does the OWASP Top 10 list name the classification for this vulnerability?

[OWASP Top 10](https://owasp.org/Top10/)

Answer: **A03:2021-Injection**

## Task 5

#### What service and version are running on port 80 of the target?

Found in initial scan

Answer: Apache httpd 2.4.38 ((Debian))

## Task 6

#### What is the standard port used for the HTTPS protocol?

Found from general knowledge

Answer: 443

## Task 7

#### What is one luck-based method of exploiting login pages?

Found from general knowledge

Answer: Brute-Forcing

## Task 8

#### What is a folder called in web-application terminology?

Found from general knowledge

Answer: Directory

## Task 9

#### What response code is given for "Not Found" errors?

Found from general knowledge

Answer: 404

## Task 10

#### What switch do we use with Gobuster to specify we're looking to discover directories, and not subdomains?

Similar question in a previous room

Answer: dir

## Task 11

#### What symbol do we use to comment out parts of the code?

Found from general knowledge

Answer: #

## Task 12

#### Submit root flag

Gobuster didn't us much unfortunately.

![](<../../../../.gitbook/assets/image (10) (1) (2).png>)

Nor did trying default passwords

Now lets try SQL Injection

SQL authentication example vulnerable to SQL Injection attacks:&#x20;

```sql
<?php
mysql_connect("localhost", "db_username", "db_password");
mysql_select_db("users");
$username=$_POST['username'];
$password=$_POST['password'];
$sql="SELECT * FROM users WHERE username='$username' AND password='$password'";
$result=mysql_query($sql);
$count=mysql_num_rows($result);
if ($count==1){
$_SESSION['username'] = $username;
$_SESSION['password'] = $password;
header("location:home.php");
}
else {
header("location:login.php");
}
?>
```

We can modify the query (the $sql variable) through the log-in form on the web page to make the query do something that is not supposed to do, bypass the authentication. We can specify the username and password through the log-in form on the web page, but it will be directly embedded in the $sql variable that performs the SQL query without input validation.

No regular expressions or functions stop us from inserting special characters, such as a single quote or pound sign. This is a dangerous practice due to those special characters can be used for modifying the queries. The pair of single quotes are used to specify the exact data that needs to be retrieved from the SQL Database, while the pound sign symbol is used to make comments. We could manipulate the query command with:

```
Username: admin'#
```

Close the query with that single quote, allowing the script to search for the admin username. Adding the pound sign, it comments out the rest of the query, which will make searching for a matching password for the specified username useless. Looking further down in the PHP authentication above, we will see that the code will only approve the login once there is one result of username AND password. Since we have skipped the password search part of our query, the script will now only search if any entry exists with the username admin. There is an account with the admin name, which will validate our SQL Injection and return the `1` value for the `$count` variable, which will be put through the if statement, allowing us to log-in without knowing the password.

With this information, we can try logging in with `admin'#`

![](<../../../../.gitbook/assets/image (1) (3) (1).png>)

![](<../../../../.gitbook/assets/image (12).png>)

Answer: **e3d0796d002a446c0e622226f42e9672**
