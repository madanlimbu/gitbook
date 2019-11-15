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

