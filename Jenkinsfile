pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Setup APIM Environments'){
            steps{
                sh './config-apim-envs.sh'
            }
        }
        stage('Build') {
            steps {
                echo 'Building artifact....'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
    }
}