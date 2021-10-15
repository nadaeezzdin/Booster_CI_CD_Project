pipeline
{
    agent any
    stages
    {
        stage('Prep')
        {
            steps
            {
               git 'https://github.com/nadaeezzdin/Booster_CI_CD_Project.git'
            }
        }
    
        stage('Build Docker Image')
        {
            steps
            {
                sh 'docker build -f Dockerfile -t noon01/Booster_proj:v1.0'
            }
        }
        
        stage('Push Docker Image to Dockerhub')
        {
            steps
            {
                withCredentials([usernamePassword(credentialsId:"Dockerhub", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
                {
                    sh 'docker login --username $USERNAME --password $PASSWORD'
                    sh 'docker push noon01/Booster_proj:v1.0 '
                }
            }
        }
        
    }
    post
    {
        success
        {
            slackSend (color: '00FF00', message: "THE DEPLOYMENT SUCCEEDED.")
        }
        failure
        {
            slackSend (color: '#FF0000', message: "THE DEPLOYMENT FAILED.")
        }
    }
}
