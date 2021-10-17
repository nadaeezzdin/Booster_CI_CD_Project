pipeline
{
    agent any
    stages
    {
        stage('Preparation')
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
                withCredentials([usernamePassword(credentialsId:"dockerhub", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')])
                {
                    sh 'docker login --username $USERNAME --password $PASSWORD'
                    sh 'docker push noon01/Booster_proj:v1.0 '
                }
            }
        }
        stage('Deployment')
        {
            steps
            {
                sh 'docker run -d -p 8000:8000 noon01/Booster_proj:v1.0'
            }
        }
        
    }
    post
    {
        success
        {
            slackSend (color: '00FF00', message: "Pipeline Succeeded")
        }
        failure
        {
            slackSend (color: '#FF0000', message: "Pipeline Failed")
        }
    }
}

