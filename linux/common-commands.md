# Common Commands

A reference for the Linux commands I use most. The command line feels like a lot\
to memorize at first, but you lean on a small core every day and look up the rest\
as needed.

Two habits make that lookup painless: almost every command supports `--help` for\
a quick summary of its options, and most have a full manual page available with\
`man <command>` (e.g. `man ls`).

> Tip: `command --help` is great for a fast reminder of flags, while\
> `man command` gives the complete documentation. Inside `man`, press `/` to\
> search, `n` for the next match, and `q` to quit.

### Files and directories

* `ls` - Lists files and folders in the current or a specified directory.
  * `ls` - current directory
  * `ls Downloads` - a relative path
  * `ls /usr/share/` - an absolute path
  * Handy flags: `ls -l` (long/detailed view), `ls -a` (include hidden\
    dotfiles), `ls -lh` (human-readable sizes), `ls -lt` (sort by time, newest\
    first), `ls -lS` (sort by size). They combine: `ls -lah`.
* `cd` - Changes into a specified directory.
  * `cd Downloads` or `cd /usr/share`
  * `cd ~` (or just `cd`) returns to your home directory, `cd -` jumps back to\
    the previous directory, and `cd ..` moves up one level.
* `pwd` - Prints the full path of the directory you are currently in ("print\
  working directory").
* `tree` - Shows a directory as an indented tree (install with your package\
  manager). `tree -L 2` limits it to two levels deep.
* `touch` - Creates an empty file, or updates the timestamp of an existing one.
  * `touch hello-world.txt`
* `mkdir` - Makes a folder.
  * `mkdir HelloFolder`
  * `mkdir -p a/b/c` creates the whole nested path, making parent folders as\
    needed.
* `mv` - Moves a file/folder; also used to rename.
  * `mv Hello.txt Documents/Hello.txt` - moves `Hello.txt` into `Documents`
  * `mv Hello.txt Goodbye.txt` - renames `Hello.txt` to `Goodbye.txt`
* `cp` - Copies a file to a specified file/folder.
  * `cp Hello.txt Documents/` - copies `Hello.txt` into the `Documents` folder
  * `cp Hello.txt Hello.txt.bak` - makes a `Hello.txt.bak` backup
  * `cp -r MyFolder Documents/` - copies a folder **and everything inside it**\
    (recursive)
* `rm` - Removes a file.
  * `rm Hello.txt`
  * `rm -r MyFolder` removes a folder and its contents. **`rm` is permanent -**\
    **there is no recycle bin**, so double-check paths, and be extremely careful\
    with `rm -rf` (recursive + force, no prompts). Never run `rm -rf` with a\
    path you haven't read twice.
* `rmdir` - Removes an _empty_ directory (safer than `rm -r` when you expect it\
  to be empty - it refuses if it isn't).
  * `rmdir MyFolder`
* `ln -s` - Creates a **symbolic link** (a pointer to another file/folder),\
  widely used for dotfiles and shared configs.
  * `ln -s /path/to/real/file linkname`

#### Finding files

* `find` - Walks the filesystem live, so results are always current (if slower).
  * `find . -name "Hello.txt"` - by name, under the current directory
  * `find . -iname "*.pdf"` - case-insensitive, with a wildcard
  * `find /var/log -type f -mtime -1` - files modified in the last day
  * `find . -name "*.tmp" -delete` - find and delete matches
* `locate` - Searches a prebuilt index for files by name (very fast).
  * `locate Hello.txt`
  * The index is refreshed by `sudo updatedb`, so a freshly created file may not\
    appear until then. Provided by the `mlocate`/`plocate` package; `find` is the\
    slower-but-always-current alternative.
* `which` / `type` - Show where a command comes from. `which python3` prints the\
  executable's path; `type ll` also reveals aliases and shell builtins.

#### Viewing and inspecting files

* `cat` - Concatenates file(s) to standard output (prints file contents). Best\
  for short files.
  * `cat hello-world.txt`
* `less` - Opens a file in a scrollable pager - the right tool for long files.\
  Navigate with arrows/`PgUp`/`PgDn`, search with `/`, quit with `q`.
  * `less /var/log/syslog`
* `head` / `tail` - Show the first/last lines of a file (10 by default).
  * `head -n 20 file.txt` - first 20 lines
  * `tail -n 50 file.txt` - last 50 lines
  * `tail -f logfile` - **follow** a file, printing new lines as they're written\
    (invaluable for watching logs live)
* `wc` - Counts lines, words, and bytes. `wc -l file.txt` counts lines.
* `grep` - Searches file(s) for keywords/patterns; often piped from another\
  command.
  * `grep dog hello-world.txt` - search a file directly
  * `cat hello-world.txt | grep dog` - search piped input
  * See SED, AWK, and Grep for a deeper dive into grep, sed, and awk.

### Redirection, pipes, and wildcards

Small operators that combine commands are where the shell gets its power.

* `>` - Redirects a command's output to a file, **overwriting** it if it exists.
  * `echo "Hello" > Hello.txt`
* `>>` - **Appends** a command's output to a file (creates it if missing).
  * `echo "Hello" >> Hello.txt`
* `|` - Pipe: sends the output of one command as the input of the next.
  * `cat Hello.txt | grep dog | wc -l` - count matching lines
* `2>` / `&>` - Redirect error output (`2>`) or both output and errors (`&>`).
  * `command > out.log 2> err.log` - split normal output and errors
* `&&` / `||` - Run the next command only if the previous **succeeded** (`&&`)\
  or **failed** (`||`).
  * `mkdir build && cd build` - only `cd` if the `mkdir` worked
* **Wildcards (globbing)** - the shell expands these before running the command:\
  `*` matches any characters, `?` a single character, and `[...]` a set.
  * `ls *.txt`, `rm log_2025-0?.csv`, `cp img_[12].png backup/`

### Networking

* `ip` - Shows or manipulates routing, devices, and tunnels. The modern,\
  more powerful replacement for `ifconfig`/`route`/`arp`.
  * `ip address` (or `ip a`) - show interfaces and IP addresses
  * `ip route` (or `ip r`) - show the routing table
  * `ip neigh` - show the ARP/neighbor cache
* `ifconfig` - Interface config: shows IP address, name, MAC address, etc. Being\
  phased out in favor of `ip` (it's in the older `net-tools` package, not\
  installed by default on many modern distros).
* `iwconfig` - Like `ifconfig` but for wireless interfaces (SSID, signal, etc.).\
  The modern equivalent is `iw`.
* `ssh` - Secure Shell: remotely and securely connect to another machine.
  * `ssh user@ip`
  * `ssh -p 2222 user@host` - use a non-default port
  * Pairs well with tmux on the remote host so your session survives a\
    dropped connection.
* `scp` / `rsync` - Copy files over SSH. `rsync -av src/ user@host:dest/` is the\
  efficient choice for anything repeated - it only transfers what changed.
* `ping host` - Quick reachability test (is the host up and routable?).
* `curl` / `wget` - Fetch URLs from the command line. `curl -O <url>` downloads\
  a file; `wget <url>` does the same with a simpler interface.
* Legacy tools you may still see: `route` (use `ip route`) and `arp` (use\
  `ip neigh`).

### Processes and the system

* `ps aux` - Snapshot of all running processes.
* `top` / `htop` - Live, interactive view of processes and resource use. `htop`\
  (install separately) is friendlier - scroll, search, and kill from the UI.
* `kill` / `killall` - Stop a process. `kill <PID>` asks it to stop politely;\
  `kill -9 <PID>` forces it; `killall firefox` targets by name.
* `df -h` - Free disk space per filesystem, human-readable.
* `du -sh <dir>` - Total size of a directory (`-s` summarize, `-h` readable).
* `free -h` - Memory usage.
* `uname -a` - Kernel and system info; `lsb_release -a` shows the distro version.

### Services (systemd)

Most modern distros use **systemd**, managed with `systemctl`. The older\
`service` command still works as a wrapper on many systems. Running these\
usually requires `sudo` - see Permissions and sudo.

* `sudo systemctl start <service>` - Start a service now.
  * `sudo systemctl start pcscd`
* `sudo systemctl stop <service>` - Stop a service now.
* `sudo systemctl restart <service>` - Restart it (e.g. after a config change).
* `sudo systemctl enable <service>` - Start the service automatically on boot.
  * `sudo systemctl enable --now pcscd` enables **and** starts it in one step.
* `sudo systemctl disable <service>` - Don't start the service on boot.
* `systemctl status <service>` - Show whether a service is running, plus recent\
  logs. (Older equivalents: `sudo service pcscd start` / `stop`.)
* `journalctl -u <service>` - Read a service's full logs; add `-f` to follow\
  them live, like `tail -f`.

### Installing / updating / upgrading

How you install, update, and upgrade software depends on your distribution's\
package manager. These commands change the whole system, so they need `sudo` -\
see Permissions and sudo for why.

#### Debian-based distros (Ubuntu, Kubuntu, Mint, Kali, …)

* `sudo apt update` - Refreshes the list of available packages from the\
  repositories (does **not** install anything yet).
* `sudo apt upgrade` - Installs the newest versions of already-installed\
  packages. Run it after `apt update`.
* `sudo apt install <package>` - Installs a package.
  * `sudo apt install git`
  * `-y` auto-confirms prompts: `sudo apt install -y git`
* `sudo apt remove <package>` - Removes a package (keeps its config files;\
  `sudo apt purge <package>` removes those too).
* `apt search <term>` - Find a package by keyword.

#### Arch-based distros (Arch, Manjaro, …)

* `sudo pacman -S <package>` - Installs a package (`-S` = sync).
* `sudo pacman -Syu` - Syncs the package database and upgrades the whole system\
  (the standard way to update a rolling-release Arch box).
* `sudo pacman -R <package>` - Removes a package (`-Rns` also removes its\
  dependencies and config).
* `pacman -Ss <term>` - Search for a package.

#### Fedora / RHEL-based distros

`dnf` is the modern tool; `yum` is the older name and still works on many\
systems.

* `sudo dnf upgrade` - Upgrades installed packages.
* `sudo dnf install <package>` - Installs a package.
* `sudo dnf remove <package>` - Removes a package.
* `dnf search <term>` - Search for a package.

> For installing Python command-line tools specifically, prefer `pipx` over the\
> system package manager - see Python Pip Pipx Venv.

### Aliases

Aliases are shortcuts for longer commands, and can even replace existing\
commands. They live either in your shell's config file (`.zshrc` for Zsh,\
`.bashrc` for Bash - the two most common shells) or in a dedicated alias file\
(such as `.bash_aliases`). Add them there so they persist across new terminals,\
then reload with `source ~/.zshrc` (or just open a new terminal). These config\
files are themselves dotfiles worth versioning - see Linux General > Dotfiles.

Some examples:

* `alias upd='sudo apt update && sudo apt upgrade -y'` - type `upd` to refresh\
  repositories and upgrade installed packages in one go, without being prompted.
* `alias ffs='sudo $(fc -l -n -1)'` - if you ran a command that needed `sudo`,\
  `ffs` re-runs that last command with `sudo` ("for... sake"). This is the alias\
  version of the built-in `sudo !!` (see Permissions and sudo > Handy sudo tips).
* `alias ..='cd ..'` - go up one directory.
* `alias ...='cd ../..'` - go up two directories.
* `alias ll='ls -lah'` - a detailed, human-readable listing including dotfiles.

To see what an alias expands to, run `type <name>` (e.g. `type upd`). To run a\
command's original version, ignoring any alias, prefix it with a backslash:\
`\ls`.

### Related notes

* Permissions and sudo - who can run what, and how to step up to root.
* SED, AWK, and Grep - searching and transforming text in pipelines.
* TMUX - keep these commands running in persistent sessions.
* Linux - the hub for all of these notes.
