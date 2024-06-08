# Test
```bash
docker build -t jenkins-docker .
docker run -d -p 8081:81 -p 50000:50000 --name jenkins-docker jenkins-docker
```

```bash
docker run --name jenkins-docker --rm --detach --privileged --network jenkins --network-alias docker --env DOCKER_TLS_CERTDIR=/certs --volume jenkins-docker-certs:/certs/client --volume jenkins-data:/var/jenkins_home --publish 2376:2376 docker:dind
```