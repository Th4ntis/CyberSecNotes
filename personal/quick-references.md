---
description: This will be a section for my quick references.
---

# 📕 Quick References

PMKID Cracking with Hashcat:

```
sudo hashcat -a X -w 3 -m 22000 (hash/file) (wordlist)/(charset)
Eg. sudo hashcat -a 0 -w 3 -m 22000 crackme.txt rockyou.txt
Eg. sudo hashcat -a 0 -w 3 -m 22000 crackme.txt ?d?d?d?d?d?d?d?d
```

