pipeline {

    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Getting source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application...'
            }
        }

        stage('Docker Build') {
            steps {
                 sh '''
                    docker build -t jenkins-cicd-app:latest .
           '''
            }
        }
        stage('Docker Push') {
             steps {
                   withCredentials([
                   usernamePassword(
                       credentialsId: 'dockerhub-credentials',
                       usernameVariable: 'DOCKER_USERNAME',
                       passwordVariable: 'DOCKER_PASSWORD'
            )
        ]) {
            sh '''
                echo "$DOCKER_PASSWORD" | docker login -u "$DOCKER_USERNAME" --password-stdin
                docker push ayishu/jenkins-cicd-app:latest
                docker logout
            '''
        }
    }
}

    }
}