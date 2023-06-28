# Hash Cracking

## What is a hash?

A hash function is any function that can be used to map data of arbitrary size to fixed-size values which can be called a hash.&#x20;

Hashing is the transformation of a string of characters into a usually shorter fixed-length value or key that represents the original string. but the hashes can’t be retrieved back to their original form as it happens in decryption.&#x20;

Both are completely different. Hashing makes it a more secure way for storing passwords. The bad thing about such “cleartext” storage of passwords is that it induces a vulnerability in the case of an attack model where the attacker could get _read-only_ access to the server data. If the website is vulnerable to SQL injection your passwords might be shown as clear text to attackers

## Hash cracking?

Hashing algorithms such as Microsoft LM hashes, MD4, MD5, SHA, MySQL, etc. make a set of mathematical operations on the clear text password (by converting it to an integer format) and produce a fixed length of the arbitrary size of data which is known as a hash.

If you input the same value to the hashing algorithm it will produce the same hash but even if you made a small change in your value the hash will be completely different.

For example:

![](<../../../.gitbook/assets/image (50) (1).png>)

![](<../../../.gitbook/assets/image (403).png>)

Notice how the `file.txt` has the word `hash` in it, and has one hash, but if he change the word to a capital H, the hash changes completely.

So what the hashing algorithms doing is, it's hashing each word with a different combination from its dictionary and comparing these hashes with our given hash until both the hashes are matched and the output is shown to us.

Basically, it's brute-forcing the hash until it finds the original hash which matches our given hash, and hence decrypting it. Keep in mind that to decrypt a hash the wordlist should contain the value you’re trying to decrypt or every possible combination should be made to decrypt the hash.

We can use many tools to crack hashes such as [JohnTheRipper](johntheripper.md), and [Hashcat](hashcat.md), and online services such as [Crackstation](https://crackstation.net/).
