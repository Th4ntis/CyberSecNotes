# Docker

## About

[Docker](https://www.docker.com/) is "an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production."&#x20;

[Docker Overview](https://docs.docker.com/get-started/overview/)

You can find Docker images [here](https://hub.docker.com/) on their Hub that you can pull and use.

## Installing

### Ubuntu

`sudo apt install docker.io docker-compose`

More info can be found [here on their docs](https://docs.docker.com/desktop/linux/install/).

### Windows

Download docker for Windows [here](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) and run the installer. When prompted, ensure the Use WSL 2 instead of Hyper-V option on the Configuration page is selected or not depending on your choice of backend.

If your system only supports one of the two options, you will not be able to select which backend to use.

More info can be found [here on their docs](https://docs.docker.com/desktop/windows/install/).

### MacOS

Download the appropriate the .dmg for the [M1 Chip](https://desktop.docker.com/mac/main/arm64/Docker.dmg?utm\_source=docker\&utm\_medium=webreferral\&utm\_campaign=docs-driven-download-mac-arm64) or [Intel Chip](https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm\_source=docker\&utm\_medium=webreferral\&utm\_campaign=docs-driven-download-mac-amd64).&#x20;

Double-click Docker.dmg to open the installer, then drag the Docker icon to the Applications folder.

Double-click Docker.app in the Applications folder to start Docker.

More info can be found [here on their docs](https://docs.docker.com/desktop/mac/install/).

## Usage

Docker commands can be found [here](https://docs.docker.com/engine/reference/commandline/cli/).

### Common Commands

* `docker run -d -t --name (name the container) (image name)` - runs the docker as as a daemon(-d) and with a pseudo-TTY (-t) with the given name(--name) from the chosen image
* `docker start (container name)` - Stars container
* `docker drop (container name)` - Stops contontainer
* `docker ps` - Shows running containers
* `docker stats` - Shows what containers are taking up what resources
* `docker pull (image)` - Pull an image or a repository from a registry
* `docker push (image:tag)` - share your images to the [Docker Hub](https://hub.docker.com/) registry or to a self-hosted one.
* `docker images` - Shows all downloaded docker images

## Examples

### Kali Linux

`sudo docker pull kalilinux/kali-rolling`

![](<../../.gitbook/assets/image (306).png>)

`sudo docker run -d -t --name kali kalilinux/kali-rolling`

![](<../../.gitbook/assets/image (310).png>)

Verify it's running. `sudo docker ps`

![](<../../.gitbook/assets/image (303).png>)

We can interact with it now by running `sudo docker exec -it Kali bash`

![](<../../.gitbook/assets/image (319).png>)

To leave the instance, type exit. Then to stop the instance, run `sudo docker stop Kali` then verify it's not running with `sudo docker ps`.

![](<../../.gitbook/assets/image (305).png>)

We can re start the instance bu running `sudo docker start Kali`.

### Ubuntu

Since Ubuntu has various versions(from 14.04 to 22.04) we can select which version we want to pull and load. Version can be found [here](https://hub.docker.com/\_/ubuntu) on the Docker hub.

`sudo docker pull ubuntu`

`sudo docker pull ubuntu:22.04`

![](<../../.gitbook/assets/image (308).png>)

![](<../../.gitbook/assets/image (304).png>)

`sudo docker run -d -t --name buntu ubuntu:20.04`

![](<../../.gitbook/assets/image (323).png>)

Verify it's running with `sudo docker ps`

![](<../../.gitbook/assets/image (322).png>)

We can interact with it now by running `sudo docker exec -it buntu bash`

![](<../../.gitbook/assets/image (314).png>)

To leave the instance, type exit. Then to stop the instance, run `sudo docker stop buntu` then verify it's not running with `sudo docker ps`.

![](<../../.gitbook/assets/image (312) (1).png>)
