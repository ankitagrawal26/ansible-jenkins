pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/ankitagrawal26/ansible-jenkins.git'
                 }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('demo-automation')
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
