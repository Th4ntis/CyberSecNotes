# Docker

[Docker](https://www.docker.com/) helps developers build, share, run, and verify applications anywhere with containers. More info on containers [here](https://www.docker.com/resources/what-container/).

A **container** is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another.

A Docker container **image** is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

This can be used on other operating systems and services such as [Ubuntu](https://hub.docker.com/\_/ubuntu), [NGINX](https://hub.docker.com/\_/nginx), [mysql](https://hub.docker.com/\_/mysql), and so many more here on [Docker Hub](https://hub.docker.com/).

[Docker Overview](https://docs.docker.com/get-started/overview/)

You can find Docker images [here](https://hub.docker.com/) on their Hub that you can pull and use.

## Installing

### Debian based Linux

```bash
sudo apt install docker.io docker-compose
```

More info for linux installation can be found [here on their docs](https://docs.docker.com/desktop/linux/install/).

### Windows

Download docker for Windows [here](https://desktop.docker.com/win/main/amd64/Docker%20Desktop%20Installer.exe) and run the installer. When prompted, ensure the Use WSL 2 instead of Hyper-V option on the Configuration page is selected or not depending on your choice of backend.

If your system only supports one of the two options, you will not be able to select which backend to use.

More info for Windows installation can be found [here on their docs](https://docs.docker.com/desktop/windows/install/).

### MacOS

Download the appropriate the .dmg for the [M1 Chip](https://desktop.docker.com/mac/main/arm64/Docker.dmg?utm\_source=docker\&utm\_medium=webreferral\&utm\_campaign=docs-driven-download-mac-arm64) or [Intel Chip](https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm\_source=docker\&utm\_medium=webreferral\&utm\_campaign=docs-driven-download-mac-amd64).

Double-click Docker.dmg to open the installer, then drag the Docker icon to the Applications folder.

Double-click Docker.app in the Applications folder to start Docker.

More info for MacOS installation can be found [here on their docs](https://docs.docker.com/desktop/mac/install/).

## Usage

Docker commands can be found [here](https://docs.docker.com/engine/reference/commandline/cli/).

### Common Commands

* Pull an image or a repository from a registry

```bash
sudo docker pull (image)
```

* List pulled images

```bash
sudo docker images
```

* Run a docker image with the given name (--name) from the chosen image

```bash
sudo docker run --it --name (name the container) (image_name)
```

* Start a container to have it run in the background

```bash
sudo docker start (container_id)
```

* Stop a running container

```
sudo docker stop (container_id)
```

* Show running containers

```bash
sudo docker ps
```

* Shows what containers are taking up what resources

```bash
sudo docker stats
```

* Share your images to the [Docker Hub](https://hub.docker.com/) registry or to a self-hosted one.

```bash
sudo docker push (image:tag)
```

* Shows all docker images

```bash
sudo docker images
```

* Removes a container

```bash
sudo docker rm [container_id]
```

* Removes an Image

```bash
sudo docker image rm [image_name]
```

### Image versions

Some images may have various versions, we can select which version we want to pull and load. Eg. Ubuntu versions can be found [here](https://hub.docker.com/\_/ubuntu) on the Docker hub and we can pull a specified Ubuntu image version with

```bash
sudo docker pull ubuntu:22.04
```

and run it with

```bash
sudo docker run --it --name ubuntu ubuntu:20.04
```

Verify it's running with

```bash
sudo docker ps
```

We can now interact with it by running

```bash
sudo docker exec -it buntu
```
