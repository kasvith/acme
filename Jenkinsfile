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
                echo 'Remove old cache...'
                sh 'rm -rf $HOME/.wso2apimcli/exported/*'
                sh 'mkdir -p $HOME/.wso2apimcli/exported/apis'
                sh 'zip -r $HOME/.wso2apimcli/exported/apis/PizzaShackAPI-1.0.0.zip PizzaShackAPI-1.0.0'
                echo 'Deploying to Production'

                withCredentials([usernamePassword(credentialsId: 'apim', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh '$(pwd)/apimcli import-api -f PizzaShackAPI-1.0.0.zip -e prod -u $USERNAME -p $PASSWORD -k --preserve-provider=false'
                }
            }
        }
    }
}