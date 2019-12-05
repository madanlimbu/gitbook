# Docker

## Networks

By default a bridge network is created.

A container's hostname defaults to be the container's ID in Docker.

### Docker network connections

#### Host to Docker

* Docker publish port \( `-p 8080:80`  \)
  * Host port 8080 to Container port 80 
  * This creates a firewall rule which maps a container port to a port on the Docker host

#### Docker to Host

* `host.docker.internal` from the docker will always point at Host machine localhost

#### Docker to Docker

* We can expose 2 different container ports to Host \(localhost\) and using `host.docker.internal` we can connect each other 
  * e.g: `container-1 8080:80` , `container-2 8081:80`  & from `container-1` can connect to `container-2` using `host.docker.internal:8081` 
* Creating docker within same network 
  * Open 2 container in same network 
  * Both container should be able to access each other using the container name

## Handy Useful commands

#### Basics

* `docker system <COMMAND>` -  **Manage Docker**
  * `df` - Show docker disk usage
  * `prune` - Remove \(containers/image/networks\) \(unreferenced/dangling\)
    * `-a` - selects all not just dangling images
    * `--volumes` - remove volumes as-well
* `docker ps` - **List Container**
  * `-a` - show all containers, not just the one running
  * `-q` - show only ID information of containers
* `docker exec` - **Run cmd in a Container**
  * `-i` - Keep STDIN open \(Interactive\)
  * `-t` - Allocate a pseudo-TTY 

#### Composition

* `docker stop $(docker ps -q)` - Stop all running containers
* `docker exec -it <CONTAINER> bash` - Use container shell

#### Sites:

* [https://www.howtogeek.com/428174/what-is-a-tty-on-linux-and-how-to-use-the-tty-command/](https://www.howtogeek.com/428174/what-is-a-tty-on-linux-and-how-to-use-the-tty-command/)
* [https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
* [https://devhints.io/docker](https://devhints.io/docker)

