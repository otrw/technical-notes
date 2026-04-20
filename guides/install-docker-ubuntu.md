# Install Docker on Ubuntu

## About

>These notes only reflect the last time Docker was installed on my homelab server. 

> Check the offical docs first for current steps:
>https://docs.docker.com/engine/install/ubuntu/

## Remove previous installed versions

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

## Set up the app repo + GPG key

```bash
sudo apt-get update
sudo apt-get install -y ca-certificates curl 
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

## Add apt sources

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

## Install Docker

```bash
sudo apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose docker-compose-plugin 
```

5. Enable non-root use

```bash
sudo usermod -aG docker $USER
newgrp docker
```

<details>

<summary>Explanation</summary>

- Adding yourself to the docker group lets you run `docker` without `sudo`
- `newgrp docker` applies the change right away, instead of logging out/in  
- If you skip this, you’ll see permission denied errors.

</details><br>

## Test install

```bash
docker run hello-world
```
