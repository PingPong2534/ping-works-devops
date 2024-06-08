# Test
```bash
docker build -t jenkins-docker .
docker run -d -p 8081:81 -p 50000:50000 --name jenkins-docker jenkins-docker
```