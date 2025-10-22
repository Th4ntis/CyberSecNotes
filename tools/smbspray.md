# SMBSpray

## About

SMB Password Sprayer

Three log files get written to the current directory when ran:

* `spray_logs.txt` - log of all attempts with timestamps
* `valid_creds.txt` - valid credentials
* `attempted_pws.txt` - passwords attempted

### Links

[Github](https://github.com/absolomb/smbspray)

## Usage

```
python3 smbspray.py -u users.txt -p passwords.txt -ip DC-IP
```

By default smbspray will attempt one password every 30 minutes, this can be tuned with the `-l` option for how often you want to spray and also `-a` for how many attempts per period you want to try. So if you want to do 5 attempts every 15 minutes do `-l 15 -a 5`. To be extra safe in case you mess this up, there is an prompt to confirm before proceeding.

```
python3 smbspray.py -u users.txt -p passwords.txt -ip DC-IP -l 15 -a 5
```
