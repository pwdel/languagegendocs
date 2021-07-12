# Language Generator Programs Documentation

Author: Patrick Delaney, July 2021

| Description / Purpose | Badge                                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Language Models       | ![](https://img.shields.io/badge/transformers-4.5.1-blue)                                                                         |
| DNN Toolkit           | ![](https://img.shields.io/badge/tensorflow-2.2-blue)                                                                             |
| Web App               | ![](https://img.shields.io/github/stars/pallets/flask?label=flask&logo=flask) ![](https://img.shields.io/badge/flask-v1.1.2-blue) |
| Database Mapper       | ![](https://img.shields.io/badge/SQLAlchemy-2.4.1-blue)                                                                           |
| Container Image       | ![](https://img.shields.io/badge/docker--python-3.8--slim-brightgreen)                                                            |
| Database Adapter      | ![](https://img.shields.io/badge/psycopg2--binary-2.8.6-red)                                                                      |

# Table of Contents



# Repos Covered and General Description

## Repo Description

### General Description

| Item                        | Link                                           | Description                                                                                                                                                                            |
|-----------------------------|------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| src flask (or source flask) | [src flask](https://github.com/pwdel/srcflask) | A fully functional application which serves as a breadcrumb along the journey to creating a fully secured, deployable language generation application using python-flask and postgres. |


    What your application does,
    Why you used the technologies you used,
    Some of the challenges you faced and features you hope to implement in the future.

### Main Breakdown of Features

* Built in python-flask, which is a largely, "from scratch," platform which allows source code to be embedded within the application project structure, making it superior for machine learning or language processing/generation applications. [Python is widely used in machine learning applications, flask is a web application platform which does not restrict database architecture or project folder structure to any particular layout, as would be the case in for example, python-django.]
* User classes separated into admin, sponsor and editors, with the admin having the capability to approve or reject the other two types of users prior to their activation within the system, allowing built-in resource protection.
* Built-in common security vulnerability prevention, which flask does not come with, "out of the box," with a full analysis of which security protections have been put in place and which have not at this stage of the app, and recommendations for further steps including but not limited to: 1. Decorated Routes which restrict access to certain routes to specified user types with a simple decorator. 2. 403 Error handling. 3. XSS, Cross Site Scripting protection. 4. CSRF Cross-Site Request Forgery protection. 5.SQL Injection Prohibition. 6. Directory Transversal Protection. 7. XSS Uploaded Files. 8. JSON Security. 9. Flask Security Headers. 10. Cookie Protection. 11. X content Type Options. 12. X-Frame Options. 13. X-XSS Protection. 14. HTTP Public Key Pinning. 15. Terminal Copy Paste Protection.
* Full review of all security considerations can be found [here](https://github.com/pwdel/flasksecurity#reviewing-flask-security-considerations).
* Flash shell to allow arbitrary database commands.
* SQLAlchemy integration for use with Postgres.
* Initial non-user state for greater security, e.g. initial user only created on the server itself via human command.

## System Requirements

### Badges

https://shields.io/category/dependencies



## Behind the Scenes

### Motivation

### Why Build this Project

### What Problems this Solves

### Learned Along the Way



# Getting Started - How to Install and Run

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
# build the web service

$ sudo docker-compose up --detach --build web

```
The above should download all dependencies and build the entire, "container environment" along with the application which gets built on top of that container environment.  If you're not familiar with containers, I recommend reading [this](https://en.wikipedia.org/wiki/Docker_(software)). In short, a container environment is a slimmed down simulation of a linux environment, which can be run on any operating system, whether it be Windows, MacOS, Linux, etc. assuming that said operating system has the capability to run the container environment. In our case we're using the container environment called, "docker."

The reason for using containers is to eliminate some of the problems associated with moving an application from a development environment, such as a laptop, to a production environment, such as a Platform as a Service type server, such as Docker or AWS-EC2.

Once you have, "composed" the web service in detached mode using the command above, you can then inspect which, "docker images," now exist on your machine and their respective sizes. The terms, "compose, images" are specific to docker and can be read about more within the docker documentation.

```
$ sudo docker images

REPOSITORY         TAG               IMAGE ID       CREATED          SIZE
userlevels_flask   latest            2c8777dd50f9   29 minutes ago   2.53GB
python             3.8-slim-buster   0e0d73ddd34d   12 days ago      114MB
postgres           13-alpine         d3a70afcf848   2 weeks ago      191MB
```
The "python" image is a base image upon which our application image, userlevels_flask was constructed on.

* Essentially, "python," is a slimmed down version of a linux system which has python installed.
* The, "postgres," image follows the same concept, but with a postgres database installed.
* "userlevels_flask" is our custom application which leverages these two below base images, as well as some other dependencies, including tensorflow, which is part of the reason for the large size of 2.53GB.
* A, "normal" flask docker application may only be perhaps in the 100MB or less range, but because we're leveraging tensorflow, which has a base size of around 2.5GB or so, depending upon the version, we have a fairly large size to our image shown above.

The images form instruction sets upon which, "processes," get built, the processes run the application. To inspect the processes running, run the command in terminal:

```
# process inspection command

$ sudo docker ps -a

| CONTAINER ID | IMAGE              | COMMAND                | CREATED           | STATUS           | PORTS                                     | NAMES |
|--------------|--------------------|------------------------|-------------------|------------------|-------------------------------------------|-------|
| b45d45623de2 | userlevels_flask   | "/usr/src/theapp/ent…" | About an hour ago | Up About an hour | 0.0.0.0:5000->5000/tcp, :::5000->5000/tcp | flask |
| c294603339c1 | postgres:13-alpine | "docker-entrypoint.s…" | About an hour ago | Up About an hour | 5432/tcp                                  | db    |


```

The processes shown above are:

* The database, named, "db" and run using postgres on alpine linux.
* The application, named "flask" with image name "userlevels_flask"

The endpoint for the application itself is found at:

```
http://0.0.0.0:5000/login
```

Which, if you visit in your browser should bring up the main front-end, endpoint of the application, which should look like this:

![](/img/loginpage.png)

The application is designed to be secured through a multi user-type categorization, which means that an administrator user type has the capability to accept or reject other user types prior to their application access. However in development mode, we have a pre-set administrator user which can be accessed via the /login page with the following credentials:

```
user: admin@test.com
password: password
```

Upon logging in as an administrator, the main dashboard shows a couple different options:

![](/img/admindashboard.png)

However, in order to see any pending issues or data within the, "Signup Requests Dashboard" option, we have to go back to the main sign-in page and request to sign up either as a sponsor or as an editor.

There are a couple of ready-made pre-approved sponsor and editor users on development mode which can be used to log in immediately:

```
# sponsor user
user: test@test.com
password: 123456

# editor user
user: editor@test.com
password: 123456

```

Logging out and returning to the front page, by clicking the, "Sign Up as Sponsor," link we can go in and create a requested sponsor-user.

![](/img/sponsorsignup.png)

Pending users

![](/img/pendingusers.png)

# How to Use

### Generating Text

https://user-images.githubusercontent.com/13304149/125302671-c7ae0b80-e2f1-11eb-8dbe-c770defa6afa.mp4

### Viewing and Editing Previously Created Documents

https://user-images.githubusercontent.com/13304149/125322446-6a22ba80-e303-11eb-9580-1784bccc8858.mp4


### Playing the Editor Role

https://user-images.githubusercontent.com/13304149/125322553-8888b600-e303-11eb-8b1d-49bbf5f033c2.mp4

### Allowing Pending Users

https://user-images.githubusercontent.com/13304149/125322643-9d654980-e303-11eb-8a81-3d6a9d8a0a0f.mp4



## Flask Shell


# About the Math Behind the Text Generation


#


# Credits

# License
