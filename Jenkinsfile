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
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                bat "docker tag node-app-test-new ${env.dockerHubUser}/node-app-test-new:latest"
                bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                bat "docker push ${env.dockerHubUser}/node-app-test-new:latest"
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
