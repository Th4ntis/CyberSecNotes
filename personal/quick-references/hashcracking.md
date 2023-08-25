# Hashcracking

### NTLM:

`hashcat -m 1000 hashes.txt rockyou.txt -O`

### NTLMv2:

`hashcat -m 5600 hashes.txt rockyou.txt -O`

### Kerberoast:

`hashcat -m 13100 kerb.txt rockyou.txt -O`

### AS-REP:

`hashcat -m 18200 asrep.txt rockyou.txt -O`

### WPA/PMKID

`hashcat -m 22000 wpa.txt rockyou.txt -O`
