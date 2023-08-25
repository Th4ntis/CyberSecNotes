# Common commands

## Built in

Some of the most common and used linux commands are listed below. all of these commands and be followed by --help for more information and additional arguments.

* `ls` - Lists files and folders in current or specified directory.
  * `ls` or `ls Downloads` or `ls /usr/share/`
* `cd` - changes into specified directory.
  * `cd Downloads` or `cd /usr/share`
* `touch` - Creates a file.
  * `touch hello-world.txt`
* `mkdir` - Makes a folder.
  * `mkdir HelloFolder`
* `mv` - Moves a file/folder, also used to rename a file/folder.
  * `mv Hello.txt Documents/Hello.txt # moves the file Hello.txt into the Documents folde`r
  * `mv Hello.txt Goodbye.txt # renames the Hello.txt file to Goodbye.txt`
* `cp` - Copies a file to a specified file/folder.
  * `cp Hello.txt Documents/ # copies the Hello.txt file into the Documents folder`
  * `cp Hello.txt Hello.txt.bak # copies the Hello.txt file to a Hello.txt.bak file`
* `cp -r` - Copies a folder
  * `cp -r MyFolder Documents/ # copies the MyFolder folder into Documents`
* `locate` - Searches for files/folders
  * `locate Hello.txt`
* `rm` - Removes a file.
  * `rm Hello.txt`
* `rmdir` - Removes a directory.
  * `rmdir MyFolder`
* `>`- Redirects the output of a command to a file and overwrites the file if it already exists.
  * `echo "Hello" > Hello.txt`
* `>>` - Appends output of a commend to the specified file
  * `echo "Hello" >> Hello.txt`
* `grep` - Search file(s) for specified keyword(s). usually piped into another command.
  * `cat hell-world.txt | grep dog`
* `cat` - Concatenate file(s) to standard output.
  * `cat hello-world.txt`
* `ifconfig` - Interface config, shows interface options, such as IP address, name, MAC address, and more.
* `iwconfig` - Similar to ifconfig but focuses on wireless interfaces.
* `ip` - used to show or manipulate routing, devices, and tunnels. Similar to ifconfig but is much more powerful with more functions and facilities.
* `ssh` - secure shell - remotely connect to another machine
  * `ssh user@ip`

## Alias

Setting alias can be simple but can get more complicated. Aliases are basically shortcuts to other commands, but can also replace commands. These can go into 2 places, your shell(ZSH or bash usually but there are plenty others out there) or into an alias file(like .bash\_alias)

Some examples are:

* `alias upd='sudo apt update && sudo apt upgrade'` This will make it so when you type 'upd' it will run the command to update the repositories and upgrade the currently installed applications,
* `alias ffs='sudo $(fc -l -n -1)'` this one is for if you ype a command that needs sudo permissions, will run the last command as sudo.
* `alias ..='cd ..'` will go up one directory.
* `alias ...='cd ../..'` will go up two directories.

<figure><img src="../../.gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>
