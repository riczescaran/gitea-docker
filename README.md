# Gitea + NGINX Reverse Proxy

## Requirements
- docker
- docker-compose
- linux distro 
> WSL can also be used in a Windows environment. To be able to run Docker within a WSL distribution, you need to enable integration on your Docker desktop.

## Installation
1. Adjust your `/etc/host` and set
```sh
127.0.0.1 gitea.docker
```

2. Create `.env` file from `.env.example` and adjust the variables to your needs. 

3. Start the docker container

```sh
docker-compose up -d
```

4. Open your browser and open http://gitea.docker for the Gitea installation.


## Enable SSH
1. Create user `git` from the host OS
```sh
sudo adduser git
```

2. Make sure that the git user `USER_UID` and `USER_GID` must match in `docker-compose.yml` file

```sh
sudo cat /etc/passwd
```

2. Generate key pair for git user
```sh
sudo -u git ssh-keygen -t rsa -b 4096 -C "Gitea Host Key"
```

3. Modify `/home/git/.ssh/authorized_keys` and add the public key of git user created from Step no. 2

4. Re start the docker

```sh
docker-compose up -d
```

5. You can now use ssh to clone. \
_Note: SSH public key must first be imported into your gitea account on the settings page._

> You can read more about SSH forwarding from the offical website: \
> https://docs.gitea.io/en-us/install-with-docker/#ssh-container-passthrough