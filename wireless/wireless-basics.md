# Wireless Basics

## OSA and WEP

Open System Authentication (OSA) is a process by which a computer can gain access to a wireless network that uses the Wired Equivalent Privacy (WEP) protocol. With OSA, a computer equipped with a wireless modem can access any WEP network and receive files that are not encrypted

OSA is one of two authentication architectures specified in the IEEE 802.11 wireless standard. The WEP protocol uses a static encryption key that doesn't change as each packet is sent, leaving networks vulnerable to attacks. As of 2004, IEEE has declared both WEP and OSA deprecated and obsolete authentication processes

Two methods of authentication can be used with WEP: Open System Authentication (OSA) and Shared Key authentication (SKA)

In OSA, the WLAN client does not provide its credentials to the Access Point during authentication. Any client can authenticate with the Access Point and then attempt to associate. With this, no authentication occurs. Afterwards, WEP keys can be used for encrypting data frames. At this point, the client must have the correct keys

In SKA, the WEP key is used for authentication in a four-step challenge-response handshake:

1. The client sends an authentication request to the Access Point (AP)
2. The AP replies with a clear-text challenge
3. The client encrypts the challenge-text using the configured WEP key and sends it back in another authentication request
4. The AP decrypts the response. If this matches the challenge text, the AP sends back a positive reply

After the authentication and association, the pre-shared WEP key is also used for encrypting the data frames using RC4

It might seem as though SKA is more secure than OSA since the latter offers no real authentication, but that's not the case. It is possible to derive the keystream used for the handshake by capturing the challenge frames in SKA. Meaning data can be more easily intercepted and decrypted with SKA than with OSA. If privacy is a primary concern, it is more advisable to use OSA for WEP authentication, rather than SKA. This also means that any WLAN client can connect to the AP.

Standard 64-bit WEP uses a 40 bit key (also known as WEP-40), which is concatenated with a 24-bit initialization vector (IV) to form the RC4 key.

A 64-bit WEP key is usually entered as a string of 10 hexadecimal (hex) characters. Each character represents 4 bits, 10 digits of 4 bits each gives 40 bits. Adding the 24-bit IV produces the complete 64-bit WEP key (4 bits × 10 + 24 bits IV = 64 bits of WEP key). Most devices also allow us to enter the key as 5 ASCII characters (0–9, a–z, A–Z), each of which is turned into 8 bits using the character's byte value in ASCII (8 bits × 5 + 24 bits IV = 64 bits of WEP key). This does restrict each byte to be a printable ASCII character, which is only a small fraction of possible byte values, greatly reducing the space of possible keys.

A 128-bit WEP key is usually entered as a string of 26 hex characters. 26 digits of 4 bits each, gives us 104 bits. Adding the 24-bit IV produces the complete 128-bit WEP key (4 bits × 26 + 24 bits IV = 128 bits of WEP key). Most devices also allow us to enter it as 13 ASCII characters (8 bits × 13 + 24 bits IV = 128 bits of WEP key).

152-bit and 256-bit WEP systems are available from some vendors. As with the other WEP variants, 24 bits of that is for the IV, leaving 128 or 232 bits for actual protection. These 128 or 232 bits are entered as 32 or 58 hex characters (4 bits × 32 + 24 bits IV = 152 bits of WEP key, 4 bits × 58 + 24 bits IV = 256 bits of WEP key). Most devices also allow us to enter it as 16 or 29 ASCII characters (8 bits × 16 + 24 bits IV = 152 bits of WEP key, 8 bits × 29 + 24 bits IV = 256 bits of WEP key).

## WPS

WiFi Protected Setup (WPS) is an optional certification program based on technology designed to ease the setup of security-enabled WiFi networks in home and small office environments

There are two primary approaches to network setup within WiFi Protected Setup: push-button and PIN entry. PIN entry is mandatory in all WiFi Protected Setup devices, while push-button is optional and may also be found in some devices.

### Push-button configuration (PBC)

In some WiFi Protected Setup networks, the user may connect multiple devices to the network and enable data encryption by pushing a button. The access point/wireless router will have a physical button, and other devices may have a physical or software-based button. Users should be aware that during the two-minute setup period which follows the push of the button, unintended devices could join the network if they are in range.

### PIN entry

In all WiFi Protected Setup networks, a unique PIN (Personal Identification Number) will be required for each device to join the network. A fixed PIN label or sticker may be placed on a device, or a dynamic PIN can be generated and shown on the device's display (e.g., a TV screen or monitor). The PIN is used to make sure the intended device is added to the network being set up and will help to avoid accidental or malicious attempts to add unintended devices to the network.

## WPA/WPA2/WPA3

WiFi Protected Access (WPA) is protocol implements the Temporal Key Integrity Protocol (TKIP). WEP used a 64-bit or 128-bit encryption key that must be manually entered on wireless access points and devices and does not change. TKIP employs a per-packet key, meaning that it dynamically generates a new 128-bit key for each packet

## WPA-Personal

Also referred to as _WPA-PSK_ (pre-shared key) mode, this is designed for home and small office networks and doesn't require an authentication server. Each wireless network device encrypts the network traffic by deriving its 128-bit encryption key from a 256-bit shared key. This key may be entered either as a string of 64 hex digits, or as a passphrase of 8 to 63 printable ASCII characters.

This pass-phrase-to-PSK mapping is nevertheless not binding. If ASCII characters are used, the 256-bit key is calculated by applying the Password-Based Key Derivation Function 2 (PBKDF2) key derivation function to the passphrase, using the SSID as the salt and 4096 iterations of Hash-Based Message Authentication Codes (HMAC)-SHA1.

WPA-Personal mode is available on all three WPA versions.

## WPA-Enterprise

Also referred to as _WPA-802.1X mode_, and sometimes just _WPA_ (as opposed to WPA-PSK), this is designed for enterprise networks and requires a RADIUS authentication server. This requires a more complicated setup, but provides additional security (e.g. protection against dictionary attacks on short passwords). Various kinds of the Extensible Authentication Protocol (EAP) are used for authentication.

WPA-Enterprise mode is available on all three WPA versions.

## 4 Way handshake

While authentication, some source keying material is turned into data encryption material which eventually can be used to encrypt data frames. This process of turning source keying material into data encryption material is called a 4-way handshake.

Both the client and authenticator (access point) know the PSK/PMK. But the PMK is not used to encrypt the data and a PTK has to be derived using PMK.

Here is how a handshake is made:

1. Client (aka Supplicant) PTK Creation: AP sends a message with Anonce in it. Anonce is a one-time use value per packet. Client creates its own PTK now that it has all the inputs (both MACs, PMK, Snonce (created by self) and Anonce).
2. AP PTK Creation: Supplicant sends out a message to AP back with its Snonce so that the AP can generate the same PTK as well. This message is sent with the MIC field set to 1 as a check to verify if this message is corrupted or not or if the key has changed by a man in the middle or some other reason. Supplicant also sends out an RSN IE (or PMKID)
3. Creation of group keys and transfer by AP to Supplicant: Once the PTKs are verified, Access Point derives GTK from GMK (For broadcast and multicast communication). GTK is delivered to supplicant which is encrypted with PTK. The message is sent to the supplicant to install the temporal keys and an RSN IE packet is also sent in the frame.
4. Confirmation of installation of keys: Supplicant confirms to the authenticator that keys have been installed.

In simpler words, a 4-way handshake does this:

1. AP sends Anonce to client and he creates PTK
2. Client sends Snonce to AP and he creates the same PTK
3. AP derives Group Keys and sends to Client encrypted with PTK
4. Supplicant installs the keys and sends confirmation back

This process is rather long and when a client goes out of range and comes back in range of the AP (called roaming) the process is lacking in efficiency. This is why routers host a smart roaming feature known as PMK caching.
