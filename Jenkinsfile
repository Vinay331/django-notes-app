pipeline {
    agent any 
    
    stages{
        stage("Code"){
            steps{
                echo "Cloning the code"
                git url: "https://github.com/Vinay331/django-notes-app.git", branch: "main"
                
            }
        }
        stage("build"){
            steps{
                echo "Building the image"
                
                sh "docker build -t my-note-app ."
                echo "Heelo World"
                
            }
        }
        stage("Push to Docker hub"){
            steps{
                echo "Pushing image to Docker Hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerhubPass",usernameVariable:"dockerhubUser")]){
                sh "docker tag my-note-app ${ env.dockerhubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker push ${env.dockerhubUser}/my-note-app:latest"
                
                }
                echo "PUSH DONE"
                
            }
        }
        stage("Deply"){
            steps{
                echo "Deploying the container"
                
               
                sh "docker-compose down && docker-compose up -d"
                
                echo "Deploy DONE"
                
            }
        }
    }
}
