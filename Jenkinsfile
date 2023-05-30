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
                bat "docker build . -t node-app-test-new"
            }
        }
        stage("Push to Docker Hub"){
            environment {
                    AWS_ACCESS_KEY_ID = 'AKIAURYNMI4ALTI5WS45'
                    AWS_SECRET_ACCESS_KEY = 'aj8c52dNow8rjuB4s0gPxlFNj9oDUk4wzMjCTkJsy'
                    AWS_REGION = 'us-east-1'
            }
            steps{
                // Log in to ECR using AWS CLI
                bat 'aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com'
                
                // Tag the Docker image
                bat 'docker tag my-image:latest ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/my-repo:latest'
                
                // Push the Docker image to ECR
                bat 'docker push ${AWS_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com/my-repo:latest'                
            }
        }
        stage("Deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
