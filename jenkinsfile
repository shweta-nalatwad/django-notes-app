pipeline {
    agent any 
    stages{
        stage("clonecode"){
            steps{
                echo"cloning the code"
                git url:"https://github.com/shweta-nalatwad/django-notes-app.git",branch: "main"
                
            }
            
        }
        stage("build"){
              steps{
                  echo "building the image"
                  sh "docker build -t my-note-app ."
                }
            }
        stage("push to dockerhub"){
              steps{
                  echo "pusing the image to docker hub"
                  withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubuser")]){
                   sh "docker tag my-note-app ${env.dockerHubuser}/my-note-app:latest"
                   sh "docker login -u ${env.dockerHubuser} -p ${env.dockerHubPass}"
                   sh "docker push ${env.dockerHubuser}/my-note-app:latest"
                  }
                
            }
            
        }
        stage("deploy"){
              steps{
                  echo "deploying the container"
                  sh "docker-compose down && docker-compose up -d"
                  
                
            }
        
         }
        
        }
    }
