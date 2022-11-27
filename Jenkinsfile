pipeline {
    agent any
    tools {
        maven 'm3'
        jdk 'jdk8'
    }
    environment {
        COMPANY_CODE='PRAGRA-123'
    }
    stages {
        stage('Compile') {
            steps {
                sh 'mvn compile'
            }
        }
        stage('Test') {
           steps {
               sh 'mvn test'
           }
        }
    }
    post {
        success {
            slackSend channel: 'devops-jan-2022', message: "Build for project ${JOB_NAME} is sucessfull"
        }
    }
}