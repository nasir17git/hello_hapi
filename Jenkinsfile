#!/usr/bin/env groovy

pipeline {

    agent {
        docker {
            image 'node'
            args '-u root'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
         stage('Clone repository') { 
            steps { 
                script{
                checkout scm
                }
            }
        }
        stage('Image Build') { 
            steps { 
                script{
                 app = docker.build("underwater")
                }
            }
        }
        stage('Image Test'){
            steps {
                 echo 'Empty'
            }
        }
        stage('Deploy') {
            steps {
                script{
                        docker.withRegistry('596152156334.dkr.ecr.ap-northeast-2.amazonaws.com', 'ecr:ap-northeast-2:AWScredentials') {
                    app.push("${env.BUILD_NUMBER}")
                    app.push("latest")
                    }
                }
            }
    }
  }
}
