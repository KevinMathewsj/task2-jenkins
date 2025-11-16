pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t task2-jenkins-app .'
            }
        }

        stage('Test Image') {
            steps {
                sh 'docker run --rm -d --name task2-test -p 8081:80 task2-jenkins-app'
                sh 'sleep 3'
                sh 'curl -f http://localhost:8081 || (docker logs task2-test; exit 1)'
                sh 'docker stop task2-test'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker stop task2-jenkins-app || true'
                sh 'docker rm task2-jenkins-app || true'
                sh 'docker run -d --name task2-jenkins-app -p 8080:80 task2-jenkins-app'
            }
        }
    }

    post {
        success { echo 'PIPELINE SUCCESS' }
        failure { echo 'PIPELINE FAILURE' }
    }
}
