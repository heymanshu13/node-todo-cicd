pipeline {
    agent any
    stages{
        stage("Clone Code"){
            steps{
                git url: "https://github.com/LondheShubham153/node-todo-cicd.git", branch: "master"
            }
        }
        stage("Build and Test"){
            steps{
                bat "docker build . -t my-image"
            }
        }
        stage("Push to Docker Hub"){
            environment {
                    AWS_ACCESS_KEY_ID = 'AKIAURYNMI4ALTI5WS45'
                    AWS_SECRET_ACCESS_KEY = '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'
                    AWS_REGION = 'us-east-1'
                    AWS_ACCOUNT_ID = '313023809280'
            }
            steps{
                
                bat 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com'                
               
                bat 'docker tag my-image:latest ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/my-repo:latest'                
               
                bat 'docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/my-repo:latest'                
            }
        }
        stage("Deploy"){
            steps{
                bat "docker-compose down && docker-compose up -d"
            }
        }
    }
}
