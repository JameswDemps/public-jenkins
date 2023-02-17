pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS=credentials('dockerhub')
    }

    stages {
         stage('Init') {
            steps {
                sh 'docker rm -f $(docker ps -qa)'
            }
        }
        stage('Build') {
            steps {
                sh 'chmod +x deploy.sh'
                sh './deploy.sh'
            }
        }

        stage('Push') {
            steps{
                sh "echo \$DOCKERHUB_CREDENTIALS_PSW | docker login -u \$DOCKERHUB_CREDENTIALS_USR --password-stdin"
                echo 'Login Completed'
                sh "docker tag trio-task-mysql:5.7 jamdcrazy/mytriotasksql:latest"
                sh "docker tag trio-task-flask-app jamdcrazy/mytriotaskflaskapp:latest"
                sh "docker push jamdcrazy/mytriotasksql:latest"
                sh "docker push jamdcrazy/mytriotaskflaskapp:latest"
            }
        }
    }
}