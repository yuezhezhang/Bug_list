## Docker

### Installation
1. Setup Docker's apt repository, [see](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
2. Install Docker desktop, [see](https://docs.docker.com/desktop/install/linux/ubuntu/)
3. Run docker without sudo, [see](https://docs.docker.com/engine/install/linux-postinstall/):
```
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
```
4. Verify
```
docker run hello-world
```

### Install Package inside a container
1. Install vim:
```
apt-get update
apt-get install vim
```
