# Sudo

The command `sudo` means "super user do", essentially telling the command to be run as an administrator. Some commands or scripts can only be run with 'sudo' permissions, meaning they need administrator rights. Eg. You want to install software on a Debian based linux distrobution, you use `apt`: `apt install git`, if ran by itself, it will tell you don't have the right permissions and to try as 'root' or with 'root' (administrator) permissions.

<figure><img src="../.gitbook/assets/image (140).png" alt=""><figcaption></figcaption></figure>

So we need to add "sudo" before the command, telling it to be run as "root" (administrator): `sudo apt install git`

<figure><img src="../.gitbook/assets/image (141).png" alt=""><figcaption></figcaption></figure>

After running as sudo, you will be asked for the sudo password for the user. This can only happen if your user is part of the 'sudo' group. If you are not in the sudo group, you will not be able to run anything with sudo permissions.

This won't happen every time as there is a time-out option enabled by default. Meaning you can sudo a command and while in the same terminal under a timeframe, any additional sudo commands will not ask for a password. But if you close out of the terminal or a certain time has passed, you will need to enter the sudo password again.

This can be edited by using `sudo visudo` and adding a line under: `Defaults env_reset`

`Defaults timestamp_timeout=<time-in-minutes>`

<figure><img src="../.gitbook/assets/image (143).png" alt=""><figcaption></figcaption></figure>
