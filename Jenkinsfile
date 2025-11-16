pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/KevinMathewsj/task2-jenkins.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t task2-jenkins-app .'
            }
        }

        stage('Test Docker Image') {
            steps {
                sh 'docker run --rm task2-jenkins-app ls'
            }
        }

        stage('Deploy Application') {
            steps {
                sh 'docker stop jenkins-task2-app || true'
                sh 'docker rm jenkins-task2-app || true'
                sh 'docker run -d -p 8080:80 --name jenkins-task2-app task2-jenkins-app'
            }
        }
    }

    post {
        success {
            echo "🎉 Jenkins CI/CD Pipeline Completed Successfully!"
        }
        failure {
            echo "❌ Pipeline Failed!"
        }
    }
}
