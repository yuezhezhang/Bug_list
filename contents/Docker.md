## Docker

### Installation
1. Setup Docker's apt repository, [see](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository) also [here](https://askubuntu.com/questions/1409192/cannot-install-docker-desktop-on-ubuntu-22-04)
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
  it should work for every new terminal, otherwise, please see [here](https://stackoverflow.com/questions/60991386/i-dont-have-permission-to-access-docker-and-every-new-terminal-instance-i-need) and [there](https://stackoverflow.com/questions/67123229/error-on-triying-executo-docker-compose-remotely-dial-unix-var-run-docker-sock).
  ```
  sudo setfacl -m user:$USER:rw /var/run/docker.sock
  ```

### Useful commands
1. [see](https://stackoverflow.com/questions/31697828/docker-name-is-already-in-use-by-container)
```
docker ps -a # List existing containers and their names
docker run container_name # Run a command in a **new** container
docker start container_name # Start one or more stopped containers
docker stop container_name # Stop before delete
docker rm container_name # remove a container
```

### Install Package inside a container
1. Install vim:
```
apt-get update
apt-get install vim
```

### Troubleshooting
1. [see](https://newbe.dev/got-permission-denied-while-trying-to-connect-to-the-docker-daemon-socket-at-unix-var-run-docker-sock-get-http-2fvar-2frun-2fdocker-sock-v1-24-images-json-dial-unix-var-run-docker-sock-connect-permission-denied-code-example)
