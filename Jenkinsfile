pipeline {
    agent any
    tools {
        maven 'm3'
        jdk 'jdk8'
    }
    parameters { string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '') }

    triggers{
         pollSCM('H */4 * * 1-5') 
        cron('H */4 * * 1-5') 
    }

   
    environment {
        COMPANY_CODE='PRAGRA-123'
    }
    stages {
         stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
  
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
        stage('Dev Only') {
            when{
                 branch 'dev'
            }
            steps {
                junit 'target/**/*.xml'
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
