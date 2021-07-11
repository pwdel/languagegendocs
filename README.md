# Language Generator Programs Documentation

# Repos Covered and General Description

## Repo Description

| Item                        | Link                                           | Description                                                                                                                                                                            |
|-----------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| src flask (or source flask) | [src flask](https://github.com/pwdel/srcflask) | A fully functional application which serves as a breadcrumb along the journey to creating a fully secured, deployable language generation application using python-flask and postgres. |



System Requirements

# Getting Started

All of the above repos run on Docker. [Installation instructions for Docker can be found here](https://docs.docker.com/engine/install/).

## Quickstart on Ubuntu

I originally developed all of this on Ubuntu. The quick way to get started and install on Ubuntu is the following, as of 11 July 2021:

```
# run updates

$ sudo apt-get update

# install docker

$  sudo apt-get install \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

# install docker GPG key

$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# setup stable repository

$  echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# install docker repo - run an update again just to be sure!

$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io

# test out to ensure you have installed docker with the basic hello world app

$ sudo docker run hello-world

```
Beyond the docker engine, docker-compose is also necessary. To install docker-compose, follow the instructions for Ubuntu at [this link](https://docs.docker.com/compose/install/).

Or, for a quickstart guide, follow the below (as of 11 Jul 2021).

```
# download the current stable release of docker-compose.

$ sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

# apply executable permissions to the binary

$ sudo chmod +x /usr/local/bin/docker-compose

# to test installation, check the version. The version and build should pop up if installed correctly.

$ docker-compose --version

```
Once you have installed docker-compose correctly, you can then run the actual application, by navigating to the root folder within your terminal and running the below command. The root folder is defined as the folder which contains docker-compose.yml:

```
#

$ sudo docker-compose up --detach --build web

```
