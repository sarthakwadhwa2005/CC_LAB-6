pipeline {
    agent any

    stages {

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Create Network') {
            steps {
                sh '''
                docker network rm lab-net || true
                docker network create lab-net
                '''
            }
        }

        stage('Deploy Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 nginx-lb || true
                docker run -d --name backend1 --network lab-net backend-app
                docker run -d --name backend2 --network lab-net backend-app
                '''
            }
        }

        stage('Deploy NGINX Load Balancer') {
            steps {
                sh '''
                docker run -d --name nginx-lb \
                --network lab-net \
                -p 80:80 \
                nginx
                '''
            }
        }
    }
}
