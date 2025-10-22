# About
Spider entire networks for juicy files sitting on SMB shares. Search filenames or file content - regex supported! 
## Links
[Github](https://github.com/blacklanternsecurity/MANSPIDER)
# Install
Install these dependencies to add additional file parsing capability (images and legacy documents)
```
sudo apt install tesseract-ocr antiword
```

Install ManSpider
```
pip install pipx
pipx install git+https://github.com/blacklanternsecurity/MANSPIDER
```
# Usage
You can run multiple instances of manspider at one time. This is useful when one instance is already running, and you want to search what it's downloaded (similar to grep -R). To do this, specify the keyword loot as the target, which will search the downloaded files in `$HOME/.manspider/loot`.

Matching files are automatically downloaded into `$HOME/.manspider/loot`! (-n to disable)

Search hostname/IP for files with "passw" in the name:
```
$ manspider TARGET -f passw -d DOMAIN -u USER -p 'PASSWORD'
```

Search for documents containing passwords
```
manspider TAGRGET -c passw -d DOMAIN -u USER -p 'PASSWORD'
```

Search the network for filenames that may contain creds
```
manspider TARGET -f passw user admin account network login logon cred -d DOMAIN -u USER -p 'PASSWORD'
```
