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
            steps{
                withCredentials([usernamePassword(credentialsId: 'ecr-credentials', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    bat 'docker login -u $AWS_ACCESS_KEY_ID -p $AWS_SECRET_ACCESS_KEY demo-project.amazonaws.com'
                    bat 'docker tag demo-project:latest 313023809280.dkr.ecr.us-east-1.amazonaws.com/demo-project:latest'
                    bat 'docker push 313023809280.dkr.ecr.us-east-1.amazonaws.com/demo-project:latest'
                }
            }
        }
        stage("Deploy"){
            steps{
                bat "docker-compose down && docker-compose up -d"
            }
        }
    }
}
