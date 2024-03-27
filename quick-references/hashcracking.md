# Hashcracking

### NTLM:

```bash
hashcat -m 1000 hashes.txt rockyou.txt -O
```

```bash
hashcat -m 1000 hashes.txt -r rule rockyou.txt -O
```

```bash
hashcat -m 1000 -w 3 hashes.txt -r rule rockyou.txt -O
```

### NTLMv2:

```bash
hashcat -m 5600 hashes.txt rockyou.txt -O
```

```bash
hashcat -m 5600 hashes.txt -r rule rockyou.txt -O
```

```bash
hashcat -m 5600 -w 3 hashes.txt -r rule rockyou.txt -O
```

### Kerberoast:

```bash
hashcat -m 13100 kerb.txt rockyou.txt -O
```

```bash
hashcat -m 13100 kerb.txt -r rule rockyou.txt -O
```

```bash
hashcat -m 13100 -w 3 kerb.txt -r rule rockyou.txt -O
```

### AS-REP:

```bash
hashcat -m 18200 asrep.txt rockyou.txt -O
```

```bash
hashcat -m 18200 asrep.txt -r rule rockyou.txt -O
```

```bash
hashcat -m -w 3 18200 asrep.txt -r rule rockyou.txt -O
```

### WPA/PMKID

```bash
hashcat -m 22000 wpa.txt rockyou.txt -O
```

```bash
hashcat -m 22000 wpa.txt -r rule rockyou.txt -O
```

```bash
hashcat -m -w 3 22000 wpa.txt -r rule rockyou.txt -O
```
