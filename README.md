# Language Generator Programs Documentation

# Repos Covered and General Description



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


$ sudo docker-compose up --detach --build web
