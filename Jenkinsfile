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
                echo 'Building Artifact....'
                sh 'zip -r PizzaShackAPI-1.0.0.zip PizzaShackAPI-1.0.0'
                echo 'Deploying to Production'

                withCredentials([usernamePassword(credentialsId: 'apim', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '$(pwd)/apimcli  import-api -f ./PizzaShackAPI-1.0.0.zip -e prod -u $USERNAME -p $PASSWORD -k'
                }
            }
        }
    }
}