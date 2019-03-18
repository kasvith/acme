pipeline {
    agent any
    environment {
        CI = 'true'
    }
    stages {
        stage('Setup APIM Environments'){
            steps{
                sh './config-apim.sh'
            }
        }
        stage('Deploy to Production') {
            when{
                buildingTag()
            }
            steps {
                echo 'Building API....'
            }
        }
    }
}