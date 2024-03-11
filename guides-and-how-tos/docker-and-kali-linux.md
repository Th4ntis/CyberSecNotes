# Docker and Kali Linux

[Docker](https://www.docker.com/) helps developers build, share, run, and verify applications anywhere with containers. More info on containers [here](https://www.docker.com/resources/what-container/).

A **container** is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

A Docker container **image** is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

My notes on Docker can be found [here](https://cybersec.th4ntis.com/general-info/docker).

# Introduction
This will be a guide on setting up [Kali Linux](https://www.kali.org/) in a docker container. Including pulling a new image, setting it up with prefer tools, services, configs, and a GUI if we want. Then covering how to save the image to a file to use on other machines or upload to docker hub to share.

## Links
- [Official Docker Images](https://www.kali.org/docs/containers/official-kalilinux-docker-images/)
- [Kali Rolling Docker Image](https://hub.docker.com/r/kalilinux/kali-rolling) on Docker Hub

# Using Kali Docker Images
Grab the latest rolling docker image with
```bash
sudo docker pull docker.io/kalilinux/kali-rolling
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/7b0c93c1-1093-4520-9916-d263a15ab181)

Followed by
```bash
sudo docker run -it kalilinux/kali-rolling
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/d0b736c5-9f37-41c4-9ed2-f6ec7b626178)

**NOTE:** all the images do not come with the “default” metapackage. You will need to run:
```bash
apt update && apt upgrade -y
```

# Installing tools
It’s pretty simple and basic from here - run
```bash
apt install -y [tool-name]
```

Eg. 
```bash
apt install -y nano bloodhound.py xrdp
```

# Setting up a share
To get file sharing setup between our container and host, we need to have a directory setup for that. On our host, we make a folder wherever we want. Create a quick file in that directory so we can verify the share is working after we run it.

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/c20295f4-803f-4a4e-9418-0b81c49d9fc3)

Now when running our Kali image with these parameters:
```bash
sudo docker run -v /home/th4ntis/Docker/Share:/home/share -it kalilinux/kali-rolling
```

When in our container, if we go to the /home/share directory, we can see the file we created on our host in the Share directory we made.

![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/c0041331-c9fe-4660-ad88-94f748d68981)

# Getting a Graphical User Interface(GUI)
Most the tools we run in Kali will be CLI based but sometimes we may need/want a GUI. To get a gui running we need to run
```bash
sudo docker run -it -p 13389:13389 kalilinux/kali-rolling
```

Then we install the XFCE desktop environment with
```bash
apt install -y kali-desktop-xfce xrdp
```

Since we chose port `13389` for our port to forward, we need to edit the xrdp config
```bash
nano /etc/xrdp/xrdp.ini
```

Change the line that says
```bash
port=3389
```
to
```bash
port=13389
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/20a77e9b-2285-4110-8299-330be196c9b8)

Then start the xrdp service
```bash
service xrdp start
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/bfccd791-cb8b-44f1-ad43-ba9c21fc4924)

Verify the XRDP service is running
```bash
service xrdp status
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/604a1961-5349-440d-ac09-b27e15ee7509)

Before we start the RDP session, we need to change the root password with
```bash
passwd
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/48e587bd-3f2e-468c-8bb5-c31e522a896d)

Now we can use whatever RDP service we want to access our Kali Docker via GUI using `localhost:13389`. I'm using Remmina, but you can use any software you choose that supports RDP. 
**NOTE**: Depending on your RDP software, you will need to choose the screen resolution you want. Otherise it will default as a 600x800 resolution.
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/7977f8f4-f68b-49c7-a6e2-f3477caa2b61)
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/d41d7f23-f5c8-45ba-b21d-2257df32a0d2)


# Adding a new non-root user
Some tools don't play wel when running as root, so we should make a new user. To do this, we run
```bash
adduser [user]
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/8ef3220c-2ae2-4f48-b64b-c602efd47f26)

Type in the password, then you can press `ENTER` when asked for full name, room number, etc.

**OPTIONAL**: To add the new user to the sudoers file. This will make sure the new user can permissions with as a super user.
```bash
usermod -aG sudo [user]
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/35e0553e-e1f2-4d20-8d61-4718b3adc3d3)

We can change to the newly created user with
```bash
su [user]
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/f0909613-a81d-4a70-8f62-63d46ad9b590)

# Making a custom image
While in your container, install all your tools, setup configs, etc. **It is important to keep the container running with all your settings, tools and configs!** Exit the container and keep it running with
```bash
CTRL+P CTRL+Q
```

Then run
```bash
sudo docker commit [container_id] [image_name]
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/2890810a-653f-4e3a-8576-afded127fea0)


Save the container in an image you can transfer to other machines with
```bash
sudo docker save [image_name] > [image_name].tar
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/95d5cf59-a7f6-4012-b17f-758e8b5cc3d2)

Now load the image on the new machine with
```bash
sudo docker image load < [container_name].tar
```

Now run the new container with all of our settings
```bash
sudo docker run -it -p 13389:13389 -v /home/[user]/Docker/Share:/home/share [container_name]
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/36a09698-ec4c-493e-95c3-66b1c818e24b)

I've added that as an alias in my terminal
```bash
alias kali-docker='sudo docker run -it -p 13389:13389 -v /home/th4ntis/Docker/Share:/home/share [container_name]'
```
![image](https://github.com/Th4ntis/th4ntis.github.io/assets/53808039/91430791-5cb6-4c24-99ac-0996a1558587)

# Conclusion
That’s it! Now you have a nice, custom Kali docker image setup with our tools, users, settings, and configs that don’t require any setup or even an internet connection!
