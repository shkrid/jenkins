pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'docker build -t shkrid/nginx-alpine:base-lua .'
            }
        }
        stage('Dockerize') {
            steps {
                echo 'Dockerize..'
                sh 'env'
                sh 'export TEST="1"'
                sh 'env'
                sh 'docker build -t shkrid/nginx-alpine:custom -f Dockerfile-custom .'
                sh 'docker login -u user -p pass || true'
                sh 'docker push shkrid/nginx-alpine:custom || true'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                echo 'docker-machine create --driver virtualbox test'
                echo 'eval "$(docker-machine env test)"'
                echo 'docker run -d -p 80:80 shkrid/nginx-alpine:custom'
            }
        }
    }
}
