# Docker

### Install docker
Ref: https://docs.docker.com/engine/install/debian/


```
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

```
```
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
sudo apt-get update
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```




## Outputs
## Check docker version info
```
root@instance-template-debian-1:/home# docker --version
Docker version 23.0.1, build a5ee5b1
root@instance-template-debian-1:/home# 
```

```
root@instance-template-debian-1:/home# docker --info
unknown flag: --info
See 'docker --help'.

Usage:  docker [OPTIONS] COMMAND

A self-sufficient runtime for containers

Common Commands:
  run         Create and run a new container from an image
  exec        Execute a command in a running container
  ps          List containers
  build       Build an image from a Dockerfile
  pull        Download an image from a registry
  push        Upload an image to a registry
  images      List images
  login       Log in to a registry
  logout      Log out from a registry
  search      Search Docker Hub for images
  version     Show the Docker version information
  info        Display system-wide information

Management Commands:
  builder     Manage builds
  buildx*     Docker Buildx (Docker Inc., v0.10.2)
  compose*    Docker Compose (Docker Inc., v2.16.0)
  container   Manage containers
  context     Manage contexts
  image       Manage images
  manifest    Manage Docker image manifests and manifest lists
  network     Manage networks
  plugin      Manage plugins
  scan*       Docker Scan (Docker Inc., v0.23.0)
  system      Manage Docker
  trust       Manage trust on Docker images
  volume      Manage volumes

```

## Docker Images

```
root@instance-template-debian-1:/home# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
ubuntu       latest    08d22c0ceb15   2 weeks ago   77.8MB
```
## Docker bash into image (-it interactive mode)
```
root@instance-template-debian-1:/home# docker run -it ubuntu /bin/bash
root@4e4757c5c74f:/# cat /etc/os-release 
PRETTY_NAME="Ubuntu 22.04.2 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04.2 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
root@4e4757c5c74f:/# 
```

## Docker search from CLI

```
root@instance-template-debian-1:/home# docker search ubuntu
NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                           Ubuntu is a Debian-based Linux operating sys…   15751     [OK]       
websphere-liberty                WebSphere Liberty multi-architecture images …   293       [OK]       
open-liberty                     Open Liberty multi-architecture images based…   59        [OK]       
neurodebian                      NeuroDebian provides neuroscience research s…   99        [OK]       
ubuntu-debootstrap               DEPRECATED; use "ubuntu" instead                50        [OK]       
ubuntu-upstart                   DEPRECATED, as is Upstart (find other proces…   112       [OK]       
ubuntu/nginx                     Nginx, a high-performance reverse proxy & we…   83                   
ubuntu/cortex                    Cortex provides storage for Prometheus. Long…   3                    
ubuntu/squid                     Squid is a caching proxy for the Web. Long-t…   52                   
ubuntu/apache2                   Apache, a secure & extensible open-source HT…   55                   
ubuntu/mysql                     MySQL open source fast, stable, multi-thread…   43                   
ubuntu/redis                     Redis, an open source key-value store. Long-…   17                   
ubuntu/bind9                     BIND 9 is a very flexible, full-featured DNS…   46                   
ubuntu/prometheus                Prometheus is a systems and service monitori…   40                   
ubuntu/kafka                     Apache Kafka, a distributed event streaming …   26                   
ubuntu/postgres                  PostgreSQL is an open source object-relation…   27                   
ubuntu/zookeeper                 ZooKeeper maintains configuration informatio…   5                    
ubuntu/grafana                   Grafana, a feature rich metrics dashboard & …   7                    
ubuntu/memcached                 Memcached, in-memory keyvalue store for smal…   5                    
ubuntu/prometheus-alertmanager   Alertmanager handles client alerts from Prom…   8                    
ubuntu/dotnet-deps               Chiselled Ubuntu for self-contained .NET & A…   6                    
ubuntu/cassandra                 Cassandra, an open source NoSQL distributed …   2                    
ubuntu/dotnet-runtime            Chiselled Ubuntu runtime image for .NET apps…   5                    
ubuntu/telegraf                  Telegraf collects, processes, aggregates & w…   4                    
ubuntu/dotnet-aspnet             Chiselled Ubuntu runtime image for ASP.NET a…   3                    
root@instance-template-debian-1:/home# 
```


## Docker active continers
```
root@instance-template-debian-1:/home# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@instance-template-debian-1:/home# docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                       PORTS     NAMES
4e4757c5c74f   ubuntu    "/bin/bash"   10 minutes ago   Exited (127) 8 minutes ago             adoring_cray
```
## Docker rename container name

```
root@instance-template-debian-1:/home# docker rename 4e4757c5c74f first_container
root@instance-template-debian-1:/home# docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                       PORTS     NAMES
4e4757c5c74f   ubuntu    "/bin/bash"   11 minutes ago   Exited (127) 9 minutes ago             first_container

```

## Pull docker image (default latest)

```
root@instance-template-debian-1:/home# docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
f1f26f570256: Already exists 
84181e80d10e: Pull complete 
1ff0f94a8007: Pull complete 
d776269cad10: Pull complete 
e9427fcfa864: Pull complete 
d4ceccbfc269: Pull complete 
Digest: sha256:617661ae7846a63de069a85333bb4778a822f853df67fe46a688b3f0e4d9cb87
Status: Downloaded newer image for nginx:latest
docker.io/library/nginx:latest
root@instance-template-debian-1:/home# 
```

## Start container

```
root@instance-template-debian-1:/home# docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
nginx        latest    ac232364af84   19 hours ago   142MB
postgres     latest    2bb008a38e7c   24 hours ago   379MB
ubuntu       latest    08d22c0ceb15   2 weeks ago    77.8MB
root@instance-template-debian-1:/home# docker run --name nginx_container -it nginx /bin/bash
root@db74681d8e35:/# ls
bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@db74681d8e35:/# exit
exit
root@instance-template-debian-1:/home# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@instance-template-debian-1:/home# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                        PORTS     NAMES
db74681d8e35   nginx     "/docker-entrypoint.…"   29 seconds ago   Exited (0) 14 seconds ago               nginx_container
4e4757c5c74f   ubuntu    "/bin/bash"              22 minutes ago   Exited (127) 19 minutes ago             first_container
root@instance-template-debian-1:/home# docker start nginx_container
nginx_container
root@instance-template-debian-1:/home# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS         PORTS     NAMES
db74681d8e35   nginx     "/docker-entrypoint.…"   53 seconds ago   Up 4 seconds   80/tcp    nginx_container
```

## Docker attach or interact with container

```
root@instance-template-debian-1:/home# docker attach nginx_container
root@db74681d8e35:/# ls  
bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@db74681d8e35:/# cat /etc/os-release
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
root@db74681d8e35:/# exit
exit
root@instance-template-debian-1:/home# 
```
## Remove container

```
root@instance-template-debian-1:/home# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                          PORTS     NAMES
db74681d8e35   nginx     "/docker-entrypoint.…"   4 minutes ago    Exited (0) About a minute ago             nginx_container
4e4757c5c74f   ubuntu    "/bin/bash"              26 minutes ago   Exited (127) 23 minutes ago               first_container
root@instance-template-debian-1:/home# docker rm first_container
first_container
root@instance-template-debian-1:/home# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                          PORTS     NAMES
db74681d8e35   nginx     "/docker-entrypoint.…"   4 minutes ago   Exited (0) About a minute ago             nginx_container
root@instance-template-debian-1:/home# 
```

## Docker container edit 

```
root@instance-template-debian-1:/home# docker attach nginx_container
root@db74681d8e35:/# ls
bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@db74681d8e35:/# cd /home/
root@db74681d8e35:/home# mkdir suyash_dir
root@db74681d8e35:/home# cd suyash_dir/
root@db74681d8e35:/home/suyash_dir# touch executeShell.sh
root@db74681d8e35:/home/suyash_dir# ls
executeShell.sh
root@db74681d8e35:/home/suyash_dir# exit
exit
root@instance-template-debian-1:/home# docker diff nginx_container
C /home
A /home/suyash_dir
A /home/suyash_dir/executeShell.sh
C /root
A /root/.bash_history
root@instance-template-debian-1:/home#
```

## Create image from the edited container

```
root@instance-template-debian-1:/home# docker commit nginx_container myimage
sha256:5787e096e935a5e420b3fcc8d5d2c35747606da143029cd9608ad8eafe336c93
root@instance-template-debian-1:/home# docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
myimage      latest    5787e096e935   11 seconds ago   142MB
nginx        latest    ac232364af84   20 hours ago     142MB
postgres     latest    2bb008a38e7c   24 hours ago     379MB
ubuntu       latest    08d22c0ceb15   2 weeks ago      77.8MB
root@instance-template-debian-1:/home# docker run --name mycontainer -it myimage /bin/bash
root@8c5d4d68fc1a:/# ls
bin  boot  dev  docker-entrypoint.d  docker-entrypoint.sh  etc  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
root@8c5d4d68fc1a:/# cd /home/
root@8c5d4d68fc1a:/home# ls
suyash_dir
root@8c5d4d68fc1a:/home# cd suyash_dir/
root@8c5d4d68fc1a:/home/suyash_dir# ls
executeShell.sh
root@8c5d4d68fc1a:/home/suyash_dir# 
```

