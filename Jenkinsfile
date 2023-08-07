pipeline {
    agent any
    stages {
        stage('CLONING THE CODE FROM GITHUB') {
            steps {
                    echo "STAGE ONE CLONE THE CODE"
                    git branch: 'main', url: 'https://github.com/NEERAJ142001/django-notes-app.git'
            }
        }
        stage("MAKING  A IMAGE") {
            steps {
                echo "STAGE TWO CREATING IMAGE"
                sh "docker build -t imagexyz ."
            }
        }
        stage("PUSHING IMAGE") {
            steps {
                echo "STAGE 3 PUSHING IMAGE TO DOCKERHUB"
                withCredentials([usernamePassword(credentialsId:"dhub",passwordVariable:"hubpassword",usernameVariable:"hubusername")]){
                sh "docker login -u ${env.hubusername} -p ${env.hubpassword}"
                sh "docker tag imagexyz donvarshneydon/my_notes_app:1.1"
                sh "docker push donvarshneydon/my_notes_app:1.1"
                }  
            }
        }
        stage("DEPLOY") {
        steps {
                echo "CREATING A CONTAINER THROUGH IMAGE"
                sh "docker-compose down"
                sh "docker-compose up -d"
            }
        }    
    }
}
