pipeline {
    agent any
     tools {
          maven 'maven3'

     }
    stages {
        stage('Clean') {
            steps {
                sh 'mvn clean'
            }
        }
        stage('Build') {
            steps {
             sh 'mvn compile'
             }
        }
        stage('Parallel and archiving') {
          parallel {

            stage('Test'){
              steps {
               sh 'mvn test'
              }
            }
             stage('Archiving') {
              steps {
               sh 'echo "Artifact" > test1.txt'
                archiveArtifacts artifacts: 'test1.txt'
                }
              }
          }
        }
        stage('Package') {
            steps {
            sh 'mvn package'
            }
        }
    }
    post {
           success{
                emailext to: "shivam.saxena@knoldus.com",
                subject: "Test Email Sucess",
                body: "Test Success"
            }

            failure{
                emailext to: "shivam.saxena@knoldus.com",
                subject: "Test Email Failure",
                body: "Test Failure"
            }
    }
}