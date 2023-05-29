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
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"deadpool@1328",usernameVariable:"heymanshu13")]){
                bat "docker tag node-app-test-new ${env."heymanshu13"}/node-app-test-new:latest"
                bat "docker login -u ${env."heymanshu13"} -p ${env."deadpool@1328"}"
                bat "docker push ${env."heymanshu13"}/node-app-test-new:latest"
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
