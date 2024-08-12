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
                    docker.image('demo-automation').run('-p 80:80')
                }
            }
        }
    }
}
