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
                sh 'docker build -t shkrid/nginx-alpine:custom -f Dockerfile-custom .'
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh 'docker push shkrid/nginx-alpine:custom' 
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....commented out'
                //sh 'docker-machine create --driver amazonec2 --amazonec2-access-key AKI******* --amazonec2-secret-key 8T93C******* aws-sandbox'
                //sh 'eval "$(docker-machine env aws-sandbox)"; docker run -d -p 80:80 shkrid/nginx-alpine:custom'
            }
        }
    }
}
