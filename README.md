Parse Server deployment on Docker Swarm cluster with Promethous+Grafan for Swarm monitoring 

Tech Stack:-
Docker
Docker Swarm(Orchastration Framework)
Jenkins(Pipeline As A Code)
Prometheus + Node Exporter + CAdvisor + Grafana (Log Analysis + Monitoring)


Note:-

-> Docker version
Client:
 Version:      17.03.1-ce
 API version:  1.27
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Mon Mar 27 17:14:09 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.03.1-ce
 API version:  1.27 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Mon Mar 27 17:14:09 2017
 OS/Arch:      linux/amd64
 Experimental: true

 -> Docker API should be enable on each docker daemon
 ExecStart=/usr/bin/dockerd -H tcp://0.0.0.0:2375  -H fd://

Task Performed :-

1. Create Docker image for Parse-Server
2. Docker image should be genrated with "Dockerfile" which packed Parse Code into docker image
3. on "Jenkinsfile" you need to change you Docker Manager IP to get image build, publish and deployed
4. Docker Compose file "docker-compose-parse.yml" used to deploy stack 
5. Jenkins build job will interact with Docker Manager and deploy a stack, as Docker Stack is not available with API's
6. Create Logging stack with "docker-compose-prometheus.yml" on Docker Manager node





