# Jenkins with docker


## pull container from dockerhub

```bash
docker pull qwertmax/jenkins-with-docker:latest
```

## to start Jenkins container

```bash
docker run -p 8080:8080 -p 50000:50000 -v $(pwd)/data:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock --name jenkins -d qwertmax/jenkins-with-docker:latest
```

## to stop Jenkins container

```bash
docker stop jenkins
```

## to delete Jenkins container

```bash
docker rm jenkins
```



`Dockerfile` looke like this 

```docker
FROM jenkins/jenkins
USER root

RUN apt-get update && \
    apt-get -y install apt-transport-https \
      ca-certificates \
      curl \
      gnupg2 \
      software-properties-common && \
    curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg > /tmp/dkey; apt-key add /tmp/dkey && \
    add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") \
      $(lsb_release -cs) \
      stable" && \
   apt-get update && \
   apt-get -y install docker-ce
```
