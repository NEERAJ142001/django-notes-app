pipeline {
    agent any
    stages{
        stage("clone the code form github"){
            steps{
                git url: "https://github.com/NEERAJ142001/django-notes-app.git", branch: "main"
            }
        }
        stage("make a image of code"){
            steps{
                sh "docker build -t donvarshneydon/notes:latest ."
            }
        }
        stage("pushing image to dockerhub"){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push donvarshneydon/notes:latest"
                }
            }
        }
        stage("make a container through image"){
            steps{
                sh "docker-compose down && docker-compose up -d"
        }
            }
        }
        
    }
