# Jenkins 

## Install and start docker container

```
docker volume create jenkins_vol
```
Starting docker container

EG:

    docker container run -d \
        -p [YOUR PORT]:8080 \
        -v [YOUR VOLUME]:/var/jenkins_home \
        --name jenkins-local \
        jenkins/jenkins

* -d: detached mode
* -v: attach volume
* -p: assign port target
* --name: name of the container


```
docker run -d -p 8080:8080 -v jenkins_vol:/var/jenkins_home --name jenkins-local jenkins/jenkins
```


```
docker logs jenkins-local
```



```
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```
```
```
```