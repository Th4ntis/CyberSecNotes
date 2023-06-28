# Dancing

![](<../../../../.gitbook/assets/image (389).png>)

## Task 1

What does the 3-letter acronym SMB stand for? - `Server Message Block`

## Task 2

What port does SMB use to operate at? - `445`

## Task 3

What network communication model does SMB use, architecturally speaking? - `client-server model`

## Task 4

What is the service name for port 445 that came up in our nmap scan? - `microsoft-ds`

## Task 5

What is the tool we use to connect to SMB shares from our Linux distribution? - `smbclient`

## Task 6

What is the `flag` or `switch` we can use with the SMB tool to `list` the contents of the share? - `-L`

Using smbclient -h we can find the flag/switch

![](<../../../../.gitbook/assets/image (179).png>)

## Task 7

What is the name of the share we are able to access in the end? - `WorkShares`

Running `smbclient -L (IP)` will list the shares, using a empty password

![](<../../../../.gitbook/assets/image (292).png>)

## Task 8

What is the command we can use within the SMB shell to download the files we find? - `get`

## Task 9

Submit root flag - `5f61c10dffbc77a704d76016a22f1664`

First connect to the machine via SMB, `smbclient '\\(IP)\WorkShares'`

![](<../../../../.gitbook/assets/image (22) (1).png>)

We can see two directories, `Amy.J` and `James.P`, we can ls both directories and see James has our flag. We can `get` our flag.txt and cat it on our machine to see our flag.

![](<../../../../.gitbook/assets/image (246).png>)
