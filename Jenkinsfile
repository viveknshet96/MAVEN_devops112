pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/viveknshet96/MAVEN_devops112.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t demo-swarm:1.0 .'
            }
        }

        stage('Deploy to Docker Swarm') {
            steps {
                sh '''
                docker service rm demo_service || true
                docker service create \
                  --name demo_service \
                  --replicas 2 \
                  demo-swarm:1.0
                '''
            }
        }
    }
}

