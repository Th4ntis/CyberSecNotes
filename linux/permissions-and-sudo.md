# Permissions and Sudo

Linux is a multi-user system, so every file and directory carries **permissions**\
that decide who may read, write, or execute it. Understanding this model is the\
key to fixing "Permission denied" errors and to keeping a system secure. The\
companion idea is **`sudo`**, which lets an authorized user step up to\
administrator (root) powers to do things the permission model would otherwise\
block - installing software, editing system files, or managing services.

This note covers both halves: first the permission model and the tools that\
change it (`chmod`, `chown`), then `sudo` itself. For the commands that these\
permissions gate in everyday use, see [Common Commands](common-commands.md).

***

## Part 1 - Permissions

### Understanding permissions

`ls -la` lists everything in a directory - including hidden dotfiles - along with\
each entry's permissions, owner, group, size, and modification time.

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

**Example 1:** `.bashrc` is a file (shown by the leading `-`). The owner can read\
and write it but not execute it; the group can read it only; and all other users\
can read it only.

**Example 2:** `.config` is a directory (shown by the leading `d`). The owner can\
read, write, **and** execute (enter) it; the group can read and execute but not\
write; and the same applies to all other users.

#### Reading the `ls -la` output

Each line has several columns. For the `.bashrc` line:

| Column         | Meaning                                                                          |
| -------------- | -------------------------------------------------------------------------------- |
| `-rw-r--r--`   | File type + read/write/execute permissions for user / group / others (see below) |
| `1`            | Number of hard links to the file                                                 |
| `th4ntis`      | The file's owner                                                                 |
| `th4ntis`      | The group assigned to the file                                                   |
| `3856`         | The file size in bytes                                                           |
| `Feb 21 02:04` | Date/time of last modification                                                   |
| `.bashrc`      | File name                                                                        |

#### The permission string

The 10-character string breaks down as `[type][user][group][others]`:

```
-   rw-   r--   r--
│    │     │     └── others:  r-- → read only
│    │     └──────── group:   r-- → read only
│    └────────────── user:    rw- → read + write
└─────────────────── type:    -   → regular file  (d = directory, l = symlink)
```

Each of the three permission groups is three characters - `r` (read),\
`w` (write), `x` (execute) - and a `-` means that permission is absent. The very\
first character is the **type**: `-` for a regular file, `d` for a directory,\
`l` for a symbolic link (and occasionally `c`/`b` for device files).

For a **directory**, the three permissions mean slightly different things than\
they do for a file:

* `r` - list the directory's contents (e.g. with `ls`).
* `w` - create, rename, or delete files inside it.
* `x` - enter it (`cd`) and access the files within.

A common gotcha: you can hold `w` on a file but still be unable to delete it, because\
deleting is controlled by `w` on the _directory that contains it_, not on the\
file itself.

#### Numeric (octal) notation

Permissions are often written as three digits, where each digit is the sum of\
read (`4`), write (`2`), and execute (`1`):

| Octal | Symbolic | Meaning                |
| ----- | -------- | ---------------------- |
| `7`   | `rwx`    | read + write + execute |
| `6`   | `rw-`    | read + write           |
| `5`   | `r-x`    | read + execute         |
| `4`   | `r--`    | read only              |
| `0`   | `---`    | no access              |

Each digit, left to right, sets the permissions for **user**, **group**, and\
**others**. So `chmod 644` = `rw-r--r--` (a typical file), and `chmod 755` =\
`rwxr-xr-x` (a typical script or directory - everyone can read and run it, only\
the owner can change it).

### Modifying permissions with `chmod`

When you create a new file such as `hello.txt`, the default permissions usually\
let you read and write it, let the group read it, and let others read it (the\
exact default is set by your `umask` - see below).

To change permissions you use `chmod` ("change mode"). It accepts either the\
numeric form above or a symbolic form.

**Numeric** is quickest when you know the exact result you want:

```bash
chmod 644 file      # rw-r--r--  : owner edits, everyone else reads
chmod 755 script.sh # rwxr-xr-x  : everyone runs, only owner edits
chmod 600 secret    # rw-------  : owner only (good for keys, tokens)
chmod 777 file      # rwxrwxrwx  : full access for EVERYONE - almost always wrong
```

> `chmod 777` is a classic security mistake. If something "only works" with 777,\
> the real fix is almost always correct ownership (see `chown` below) plus a\
> tighter mode like 755 or 644.

**Symbolic** is clearest when you want to tweak one bit without recomputing the\
whole set. It needs three things:

* **Who** the change is for: `u` (user/owner), `g` (group), `o` (others), or\
  `a` (all). If you omit this, `chmod` acts as if you wrote `a`.
* **What** to do: `+` adds a permission, `-` removes one, `=` sets exactly these\
  and clears the rest.
* **Which** permission: `r`, `w`, or `x`.

Examples:

```bash
chmod +x script.sh      # make a script executable (for everyone)
chmod o-r filename      # remove read permission for "others"
chmod u+x,g-w file      # add execute for owner, remove write for group
chmod -R 755 myfolder/  # apply recursively to a whole directory tree
```

#### Default permissions and `umask`

New files don't come out as `777`/`666` because the shell subtracts a mask -\
your **`umask`** - from the base permissions. Run `umask` to see it (commonly\
`022`, which clears write for group and others, giving `755` dirs and `644`\
files). You rarely need to change it, but it's the answer to "why do my new files\
come out as `644`?"

### Changing ownership with `chown`

`chmod` changes _what_ can be done to a file; `chown` changes _who owns it_.\
Because reassigning ownership is a privileged action, it usually requires `sudo`\
(Part 2).

```bash
sudo chown th4ntis file.txt            # change the owner
sudo chown th4ntis:th4ntis file.txt    # change owner AND group
sudo chown -R th4ntis:th4ntis myfolder/ # recursively, whole tree
sudo chgrp developers file.txt         # change only the group
```

Ownership and permissions work together: permissions are evaluated against\
_&#x79;our_ relationship to the file (are you the owner? in its group? neither?), so\
the owner/group set by `chown` decides _which_ of the `rwx` triplets applies to\
you.

***

## Part 2 - sudo

`sudo` means "**su**per **u**ser **do**" - it runs a single command as the\
administrator (the **root** user). Some commands can only run as root because\
they touch things the permission model protects: installing software, editing\
files under `/etc`, or managing services (see\
Common Commands > Services (systemd)).

For example, installing software on a Debian-based distro uses `apt`. Run on its\
own it fails, because a normal user doesn't have permission to write to the\
system, and it tells you to try as root:

<figure><img src="../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

So you prefix the command with `sudo`, telling it to run that one command as\
root:

```bash
sudo apt install git
```

<figure><img src="../.gitbook/assets/image (58).png" alt=""><figcaption></figcaption></figure>

After running a `sudo` command you're prompted for **your own** password, not\
root's. This works only if your user is a member of the `sudo` group (called\
`wheel` on some distros, such as Fedora and Arch). If you aren't in that group,\
`sudo` will refuse to run anything.

> Check your group membership with `groups`. An administrator can add a user to\
> the sudo group with `sudo usermod -aG sudo <username>` (or `-aG wheel` on\
> distros that use `wheel`). The user must log out and back in for it to take\
> effect.

### The password timeout

You won't be asked for your password on _every_ `sudo` command. By default there\
is a timeout: once you authenticate, further `sudo` commands in the same terminal\
won't re-prompt for a short period (15 minutes by default). Once that time passes

* or you close the terminal - you'll be asked again.

You can change this by editing the **sudoers** file. **Always edit it with**\
**`sudo visudo`**, never a normal text editor - `visudo` checks the file for syntax\
errors before saving, and a broken sudoers file can lock you out of `sudo`\
entirely.

Add a line under `Defaults env_reset`:

```
Defaults timestamp_timeout=<time-in-minutes>
```

<figure><img src="../.gitbook/assets/image (113).png" alt=""><figcaption></figcaption></figure>

For example, `Defaults timestamp_timeout=30` keeps your authentication valid for\
30 minutes. Setting it to `0` forces a password every time; `-1` disables the\
timeout for the session (not recommended - it leaves a terminal able to run root\
commands indefinitely).

### Handy sudo tips

* `sudo !!` re-runs the **previous** command with `sudo` - perfect for when you\
  forget it. (My `ffs` alias in Common Commands > Aliases automates the same\
  idea.)
* `sudo -i` or `sudo -s` opens an interactive root shell, so you don't have to\
  prefix every command. Exit it promptly - it's easy to forget you're root and\
  do real damage.
* `sudo -l` lists exactly what commands your user is allowed to run with `sudo`.
* `sudo -k` "forgets" your cached authentication immediately, so the next `sudo`\
  re-prompts (the opposite of waiting out the timeout).
