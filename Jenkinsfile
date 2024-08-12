pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ankitagrawal26/ansible-jenkins.git'
                 }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh '''docker build -t demo-auto .'''
                }
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    sh ''' docker run -d -p 80:80 demo-auto'''
                }
            }
        }
    }
}
