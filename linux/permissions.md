# Permissions

## Understanding permissions

`ls -la`: Lists all files/folders in a directory, including hidden files/folders.

![](<../.gitbook/assets/image (393).png>)

Example1: `.bashrc` is a file(Indicated by -), and the owner can read and write to it, but not execute. The group it belongs to can read it, but not write or execute, and any other user can't do anything with the file.

Example2: `.config` is a directory(Indicated by the d), and the owner is able to read, write, AND execute, the group can read and execute, but not write, the sme goes for any other user as well.

For the `.bashrc` file:

| Column       | Meaning                                                                                   |
| ------------ | ----------------------------------------------------------------------------------------- |
| -rw-r--r--   | Indicates a file or folder, read/write/execute permissions for the user/group/other users |
| 1            | Shows number of hard links to the file                                                    |
| th4ntis      | The file owner                                                                            |
| th4ntis      | The group assigned to the file                                                            |
| 3856         | The file size in bytes                                                                    |
| Feb 21 02:04 | Date/Time of last modification                                                            |
| .bashrc      | File name                                                                                 |

## Modifying Permissions

A new file named hello.txt  By default we can only read and write, the group can do the same, other users can only read it.

![](<../.gitbook/assets/image (696).png>)

To change the permission, you run `chmod` which stand for change mode. Eg. `chmod 777` will give full read, write, execute permissions to everything and everyone.  Eg. `chmod +x` will make the file executable to everyone.

To use `chmod` to set permissions, we need to tell it:

* _Who:_ Who we are setting permissions for.
* _What_: What change are we making? Are we adding or removing the permission?
* _Which_: Which of the permissions are we setting?

The “who” values we can use are:

* _u_: User, meaning the owner of the file.
* _g_: Group, meaning members of the group the file belongs to.
* _o_: Others, meaning people not governed by the `u` and `g` permissions.
* _a_: All, meaning all of the above.

If none of these are used, `chmod` behaves as if “`a`” had been used.

The “what” values we can use are:

* _`–`_: Minus sign. Removes the permission.
* _`+`_: Plus sign. Grants the permission. The permission is added to the existing permissions. If you want to have this permission and only this permission set, use the `=` option, described below.
* _`=`_: Equals sign. Set a permission and remove others.

The “which ” values we can use are:

* _r_:  The read permission.
* _w_: The write permission.
* _x_: The execute permission.

Eg. Changing the permission to remove read permissions to a file: `chmod o-r filename`.&#x20;

Eg. Changing the file to be able to be executed: `chmod +x script.sh`
