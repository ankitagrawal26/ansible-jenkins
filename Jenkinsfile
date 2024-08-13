pipeline {
    agent any

    environment {

        SERVICENOW_INSTANCE = 'https://birlasoftindemo2.service-now.com'
        SERVICENOW_CREDENTIALS = 'servicenow-creds'
    }

    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/ankitagrawal26/ansible-jenkins.git'
            }
        }
        stage('Docker Image') {
            steps {
                script {
                    sh '''docker build -t demo-auto .'''
                 }
            }
        }
        stage('Deployment') {
            steps {
                script {
                    sh ''' docker stop bslc'''
                    sh ''' docker rm bslc'''
                    sh ''' docker run -d -p 80:80 --name bslc demo-auto'''
                 }
            }
        }
        stage('Create ServiceNow Ticket') {
            steps {
                script {
                    def response = httpRequest(
                        url: "${env.SERVICENOW_INSTANCE}/api/now/table/incident",
                        httpMode: 'POST',
                        authentication: "${env.SERVICENOW_CREDENTIALS}",
                        contentType: 'APPLICATION_JSON',
                        requestBody: '''{
                            "short_description": "New code commit detected",

                            "description": "A new code commit has been made to the repository. Please review.",
                            "category": "Software",
                            "subcategory": "Application"
                        }'''
                    )
                    echo "ServiceNow response: ${response.content}"
                }
            }
        }
    }
}

