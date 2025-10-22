# Evil Portal

## Basic Portal

I was unable to clone the repoitory to my pineapple. so I glones them ot my machine and copied them to the pineapple under `/root/portals/`. I took some of [Kleo Evil Portals](https://github.com/kleo/evilportals) as I'm not skilled enough to make my own.

```bash
git clone <https://github.com/Th4ntis/Evil-Portals.git>
scp -r Evil-Portals/* root@172.16.42.1:/root/portals/
```

Download the Evil Portal module from the Pineapple Modules

<figure><img src="../../.gitbook/assets/Pasted image 20250909133457.png" alt=""><figcaption></figcaption></figure>

Once installed open the module, and install dependencies. Now we can preview the portals by activating the Portal

<figure><img src="../../.gitbook/assets/Pasted image 20250909133502.png" alt=""><figcaption></figcaption></figure>

Once activated, start the web server, then we can preview it.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133505.png" alt=""><figcaption></figcaption></figure>

Now, we go to our OpenAP, set the desired WiFi name, BSSID, and channel.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133511.png" alt=""><figcaption></figcaption></figure>

Start the server with the Evil Portal, now when a client is connected, on the home page we will see their MAC address and IP address.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133516.png" alt=""><figcaption></figcaption></figure>

Take the IP address and add it into the Evil Portals allowed clients.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133521.png" alt=""><figcaption></figcaption></figure>

Now when the client is connected they are sent to an authorization login page, Google in the case.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133526.png" alt=""><figcaption></figcaption></figure>

If they enter their credentials, their page shows they aren't authorized.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133531.png" alt=""><figcaption></figcaption></figure>

We also get a notification our Pineapple page.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133536.png" alt=""><figcaption></figcaption></figure>

We can view the logs from the Evil Portal page to see the email, password, hostname, MAC, and IP that put in their credentials.

<figure><img src="../../.gitbook/assets/Pasted image 20250909133541.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/Pasted image 20250909133545.png" alt=""><figcaption></figcaption></figure>
