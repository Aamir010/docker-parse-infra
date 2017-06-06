pipeline {
    agent any
    parameters {
        string(name: 'DOCKER-SWARM-MANAGER', defaultValue: '192.168.0.108', description: 'Docker Swarm Manager Node IP Address')
    }
    stages {
        stage('git') {
            steps {
                git url: 'https://github.com/Aamir010/docker-parse-infra.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh '''#Leveraging Python library to interact with Docker
                      #Install Python Library with pip install docker
                      #Modify Docker deamon details as per your environment
                      #!/usr/bin/python
                      import docker
                      client = docker.DockerClient(base_url='tcp://192.168.0.108:2375')
                      build_image = client.images.build(path=${env.WORKSPACE},tag=aamir010/parse-code:${env.BUILD_NUMBER},stream=True,encoding="gzip")'''
            }
        }
        stage('Push Docker Image') {
            steps {
                sh '''#!/usr/bin/python
                      import docker
                      client = docker.DockerClient(base_url='tcp://192.168.0.108:2375')
                      for line in client.images.push('aamir010/parse-code:${env.BUILD_NUMBER}', stream=True):
                            print line
                      print "Docker Image successfully pushed to Docker Registry" '''
            }
        }
        stage('Deploy Docker Image') {
            sh '''scp docker-compose-parse.yml root@$DOCKER-SWARM-MANAGER:/home
                  ssh root@$DOCKER-SWARM-MANAGER "docker stack deploy -c /home/docker-compose-parse.yml parse-server-stack" '''
        }
    }
}