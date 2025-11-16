pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR_USERNAME/task2-jenkins-cicd.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t jenkins-cicd-app ./app'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker run -d -p 3000:3000 --name test-app jenkins-cicd-app'
                sh 'sleep 5'
                sh 'curl http://localhost:3000'
                sh 'docker stop test-app'
                sh 'docker rm test-app'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker run -d -p 3000:3000 --name production-app jenkins-cicd-app'
            }
        }

    }
}
