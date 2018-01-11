pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'env'
                sh 'docker version'
                sh 'docker build -t shkrid/nginx-alpine:base .'
            }
        }
        stage('Dockerize') {
            steps {
                echo 'Testing..'
                sh 'docker version'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                sh 'docker version'
            }
        }
    }
}
