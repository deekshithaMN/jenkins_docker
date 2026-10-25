
pipeline {
    agent any

    triggers {
        pollSCM('H/1 * * * *')
    }

    stages {
        stage('Build') {
            steps {
                bat 'docker build -t jenkins-cicd-app:latest .'
            }
        }

        stage('Test') {
            steps {
                bat 'docker image inspect jenkins-cicd-app:latest'
                bat 'findstr /C:"Jenkins CI/CD Pipeline" index.html'
            }
        }

        stage('Deploy') {
            steps {
                bat '''
                docker rm -f jenkins-cicd-app 2>NUL
                docker run -d --name jenkins-cicd-app -p 8081:80 jenkins-cicd-app:latest
                '''
            }
        }
    }
}