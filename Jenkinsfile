pipeline {
    agent any

 
    stages {
        stage('preparation') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/nadaeezzdin/Booster_CI_CD_Project.git'
                
                }
           }
            stage('docker build and push') {
            steps {
                // Get some code from a GitHub repository
                withCredentials([usernamePassword(credentialsId:"dockerhub",usernameVariable:"USERNAME",passwordVariable:"PASSWORD")]){
                sh """
                  docker build . -f dockerfile -t noon01/Booster_proj:v1.0
                  docker login -u ${USERNAME} -p ${PASSWORD}
                  docker push noon01/Booster_proj:v1.0 
                """
                }
               post {
             
               success {
                   slackSend (color: '#228B22', message: " PIPELINE SUCCEEDED.")
                }
              failure {
                 slackSend (color: '#FF0000', message: "PIPELINE FAILED.")
               }
               }    
            }
        }
    }
}
