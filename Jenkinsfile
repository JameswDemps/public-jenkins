pipeline {
    agent any
    stages {
        stage('Stop/Remove'){
            steps {
                sh 'docker stop myapp || true'
                sh 'docker rm myapp || true'
            }
        }
        stage('Build'){
            steps {
                sh 'docker build -t myapp .'
            }
        }
        stage('Deploy'){
            steps {
                sh 'docker run --rm -p 5000:5000 --name myapp -d myapp:latest'
            }
        }
    }
}