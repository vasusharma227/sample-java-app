pipeline {
    agent any
    tools {
        maven 'm3'
        jdk 'jdk8'
    }
    options {
        buildDiscarder(logRotator(numToKeepStr: '3')) 
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
            slackSend channel: 'devops-jan-2022', message: "Build for project ${BUILD_NUMBER} is sucessfull"
        }
        always {
            mail bcc: '', body: 'Hello Form Jenkins', cc: 'huzaifa.tin.edu@gmail.com', from: '', replyTo: '', subject: "Build Status for ${JOB_NAME} is ${BUILD_NUMBER}", to: 'atin@pragra.io'
        }
    }
}