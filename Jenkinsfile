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
            }
            steps {
                
                bat 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 313023809280.dkr.ecr.us-east-1.amazonaws.com'               
               
                bat 'docker tag my-image:latest 313023809280.dkr.ecr.us-east-1.amazonaws.com/my-repo:latest'                
               
                bat 'docker push 313023809280.dkr.ecr.us-east-1.amazonaws.com/my-repo:latest'                
            }
        }
        stage("Deploy"){
            steps{
                bat "docker-compose down && docker-compose up -d"
            }
        }
    }
}
