pipeline {
    agent any

    stages {
        stage('Checkout Code') {
            steps {
                echo 'Code checked out successfully'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t flask-jenkins-app .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh '''
                docker stop flask-jenkins || true
                docker rm flask-jenkins || true
                docker run -d -p 5000:5000 --name flask-jenkins flask-jenkins-app
                '''
            }
        }
    }
}
