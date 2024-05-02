# Hashcracking

### NTLM:

```bash
hashcat -m 1000 ntlm-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 1000 -w 3 ntlm-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### NTLMv2:

```bash
hashcat -m 5600 ntlmv2-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 5600 -w 3 ntlmv2-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### Kerberoast:

```bash
hashcat -m 13100 kerb-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m 13100 -w 3 kerb-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### AS-REP:

```bash
hashcat -m 18200 asrep-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 18200 asrep-hashes.txt -r rule wordlist -o Cracked.txt -O
```

### WPA/PMKID

```bash
hashcat -m 22000 wpa-hashes.txt wordlist -o Cracked.txt -O
```

```bash
hashcat -m 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```

```bash
hashcat -m -w 3 22000 wpa-hashes.txt -r rule wordlist -o Cracked.txt -O
```
