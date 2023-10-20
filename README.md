# Resources


### Jenkins GitHub: 

- <https://github.com/jenkinsci/docker>

### Pipeline systax :

- <https://www.jenkins.io/doc/book/pipeline/syntax/>

- <https://www.jenkins.io/doc/pipeline/steps/workflow-basic-steps/>

### Simple java maven app : 

- <https://github.com/jenkins-docs/simple-java-maven-app>

### Parametrized pipelines : 

- <https://github.com/jenkinsci/pipeline-model-definition-plugin/wiki/Parametrized-pipelines>

### Using environtment variables :

- <https://www.jenkins.io/doc/book/pipeline/jenkinsfile/#using-environment-variables>

### Pipeline build setup :

- <https://www.jenkins.io/doc/pipeline/steps/pipeline-build-step/>




## Using docker inside jenkins container 

1. Build docker image with a docker file 

```
docker build -t myjenkins-blueocean ./spike_container  
```

2. Run this code 

```
docker run \
  --name jenkins-blueocean \
  --restart=on-failure \
  --detach \
  --network jenkins \
  --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client \
  --env DOCKER_TLS_VERIFY=1 \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  myjenkins-blueocean
```

```
  --volume /var/run/docker.sock:/var/run/docker.sock 
  
  We mounted this docker.sock so that inside the jenkins, we are using docker socket from outside
```