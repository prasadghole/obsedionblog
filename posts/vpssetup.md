---
title: "VPS setup"
date: 2022-07-12
tags: []
publish: true
---

# VPS setup 
This page document various steps and tasks performed to manage my own vps server. I choose
VPS service from hostinger.

## Initial Setup
After registering and payment, I logged in and started server instance. I choose non default
ubuntu os. (Centos was default)

I added my personal public ssh key to account. 

## SSH Connection
[Reference](https://www.hostinger.in/tutorials/getting-started-with-vps-hosting)
Once started on vps manage page you will see ip address of my vps machine.

I ssh into it.

## Web Server
Apache was pre installed on this machine. Hence when I types ip address I was able to default 
http page. Next task is convert this to https only secured website.

## Creating new non root user
```
adduser usename
usermod -aG sudo usrname
```

SSH access for new user
```
su - username
mkdir .ssh
chmod 700 .ssh

```

Create public private key pair or use existing public key. I used my existing
public key as

```
scp ~/.ssh/id_rsa.pub username@hostname:/home/username/.ssh
```

On VPS server

```
echo ~/home/username/.ssh/id_rsa.pub >> authorized_keys
```


### Creating git user
To use VPS as git server I have created git user with 
[setting up git server](https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server)


# Setting up Jenkins
On my particular machine standard instructions for installing jenkins were not working
I followed [Install on linux](https://www.jenkins.io/doc/book/installing/linux/):w

## Install java
```
sudo apt install default-jre
```
Run jenkins
```
sudo systemctl start jenkins

```

## Starting Jenkins
Once started on http port 8080 it will ask for initial password. To get the password
## Starting Jenkins
Once started on http port 8080 it will ask for initial password. To get the password

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
Proceed with default plugin installation.

# Hosting web site
My current vps support apache webserver as default. File served from 
/var/www/html.index is my home page.

## Domain name in direction

## Setting up https secured access

Login to remote server with non root user
```
sudo apt install software-properties-common
sudo add-apt-repository ppa:certbot/certbot

sudo apt update
sudo apt install certbot python3-certbot-apache

```

# References
1. [DigitalOcean Setup](https://www.digitalocean.com/community/tutorials/how-to-install-the-apache-web-server-on-ubuntu-22-04#step-5-setting-up-virtual-hosts-recommended)
2. [DigitalOcean https](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu-22-04)
