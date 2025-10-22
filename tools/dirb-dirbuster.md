# Dirb/Dirbuster

## About

### Dirb

DIRB, also known as dirbuster and directory buster, is a Web Content Scanner. It looks for existing (and/or hidden) Web Objects. It basically works by launching a dictionary based attack against a web server and analyzing the responses. It comes with a set of preconfigured attack wordlists for easy usage but you can use your custom wordlists. Also DIRB sometimes can be used as a classic CGI scanner, but remember that it is a content scanner not a vulnerability scanner. The main purpose is to help in professional web application auditing. Specially in security related testing. It covers some holes not covered by classic web vulnerability scanners. DIRB looks for specific web objects that other generic CGI scanners can’t look for. It doesn’t search vulnerabilities nor does it look for web contents that can be vulnerable.

### Dirbuster

DirBuster is a multi threaded java application designed to brute force directories and files names on web/application servers. Often is the case now of what looks like a web server in a state of default installation is actually not, and has pages and applications hidden within. DirBuster attempts to find these.

However tools of this nature are often as only good as the directory and file list they come with. A different approach was taken to generating this. The list was generated from scratch, by crawling the Internet and collecting the directory and files that are actually used by developers! DirBuster comes a total of 9 different lists, this makes DirBuster extremely effective at finding those hidden files and directories. And if that was not enough DirBuster also has the option to perform a pure brute force, which leaves the hidden directories and files nowhere to hide.

## Installing

### Dirb:

```
sudo apt install -y dirb
```

### Dirbuster:

```
git clone https://gitlab.com/kalilinux/packages/dirbuster.git
```

## Usage

### Dirb:

* Dirb syntax

```
dirb <url_base> [<wordlist_file(s)>] [options]
```

* Example:

```
dirb http://TARGET /opt/SecLists/Discovery/Web-Content/directory-list-1.0.txt
```

* Add the -u argument to add in usernames and passwords with the -U argument.

```
dirb http://TARGET /opt/SecLists/Discovery/Web-Content/directory-list-1.0.txt -U USER:PASSWORD
```

As well as using a text file for the username/password.

### Dirbuster:

You can run the .sh or .jar file in the dirbuster directory.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FVcczzBVzNhkw32qIGAqx%252Fimage.png%3Falt%3Dmedia%26token%3D5097b3a6-f515-49e2-bcaa-38aeb93b2397\&width=768\&dpr=4\&quality=100\&sign=7dbd8fd5\&sv=2)

This can run the same things as Dirb but has a GUI and is multi-threaded, therefore tends to be faster, and more effective.

When running it be sure to specify a list of directories and/or file extentions depending on what software the server is running, like .asp or .aspcx. A good practice is to include .txt, .zip, etc but this can add more time.

![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FHapXQBGb2PPTXlLsCqfx%252Fimage.png%3Falt%3Dmedia%26token%3D245df162-93b6-4798-a3b0-1ab0d1bccbac\&width=768\&dpr=4\&quality=100\&sign=bc04e2d5\&sv=2)
