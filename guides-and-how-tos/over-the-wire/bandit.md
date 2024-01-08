# Bandit

[Bandit](https://overthewire.org/wargames/bandit/). This game is aimed at absolute beginners. It teaches the basics needed to be able to play the other games.

## Starting out

Level 0 has us SSH into to log in. We can use `ssh bandit.labs.overthewire.org -p 2220 -l bandit0` with the password of `bandit0`, as they provide the uername and password.

<figure><img src="../../.gitbook/assets/image (222).png" alt=""><figcaption></figcaption></figure>

## Level 0

Now that we're in, we need to log in using user `bandit1` now, the password is located in a file called `readme` in the home directory. So lets use ls to verify the file is there with `ls`, and `cat` the file to see it's contents.

<figure><img src="../../.gitbook/assets/image (724).png" alt=""><figcaption></figcaption></figure>

Now we can log into level 2 with `ssh bandit.labs.overthewire.org -p 2220 -l bandit1` with the new password `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`

<figure><img src="../../.gitbook/assets/image (369).png" alt=""><figcaption></figcaption></figure>

## Level 1

The password to get to level 2 is found in file - located in the home directory.

Now with this, we can't just cat the file as it starts with(is) special character, so we need to use `cat ./(character)` like this: `cat ./-`.  Now we get our next password, which is `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`.

<figure><img src="../../.gitbook/assets/image (674).png" alt=""><figcaption></figcaption></figure>

## Level 2

We can log into Level 2 with `ssh bandit.labs.overthewire.org -p 2220 -l bandit2` using the password we obtained from level 1, `rRGizSaX8Mk1RTb1CNQoXTcYZWU6lgzi`.

<figure><img src="../../.gitbook/assets/image (658).png" alt=""><figcaption></figcaption></figure>

For this game, the password for the next level is located in a file called **spaces in this filename** located in the home directory.

To cat a file with spaces in the name, we need to "breakout" using the bacspace (`\`) character at the and of each word.

<figure><img src="../../.gitbook/assets/image (538).png" alt=""><figcaption></figcaption></figure>

We can now see the password is `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`.

## Level 3

From this point on, SSHing into the new machine pics won't be posted. We can log into Level 3 with `ssh bandit.labs.overthewire.org -p 2220 -l bandit3` and using the password from the previous session, `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`.

The password for the next level is in a hidden file in the **inhere** directory. Hidden files in linux are started with a perdio (`.`) so looking in the inhere directory, we see nothing, but using ls -al we can see all the files, including hidden, in that directory. So we can cat that file to obtain the password `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`.

<figure><img src="../../.gitbook/assets/image (258).png" alt=""><figcaption></figcaption></figure>

## Level 4

Log into Level 4 with `ssh bandit.labs.overthewire.org -p 2220 -l bandit4` and using the password from the previous session, `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`.

This level, the password is in the only 'human-readable' file in the `inhere` directory.

<figure><img src="../../.gitbook/assets/image (235).png" alt=""><figcaption></figcaption></figure>

We can see the what they mean by human-readable. So, we can cat each file individually but, theres another way using the `file` command. We can run `file ./*` to identify each file type.&#x20;

<figure><img src="../../.gitbook/assets/image (699).png" alt=""><figcaption></figcaption></figure>

We see -file07 is ASCII text. So now we can cat the file to see it's contents.

<figure><img src="../../.gitbook/assets/image (303).png" alt=""><figcaption></figcaption></figure>

We can see the password is `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`.

## Level 5

Log into Level 5 with `ssh bandit.labs.overthewire.org -p 2220 -l bandit5` and using the password from the previous session, `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`.



## Level 6

## Level 7

## Level 8

## Level 9

## Level 10

## Level 11

## Level 12

## Level 13

## Level 14

## Level 15

## Level 16

## Level 17

## Level 18

## Level 19

## Level 20

## Level 21

## Level 22

## Level 23

## Level 24

## Level 25

## Level 26

## Level 27

## Level 28

## Level 29

## Level 30

## Level 31

## Level 32

## Level 33

## Level 34
