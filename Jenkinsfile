pipeline{
    agent {label "slave_node"}
    
    stages{
        stage("Code"){
            steps{
                echo "This is cloning the code"
                git url: "https://github.com/Eagle766/djnago-Notes-App.git", branch: "main"
                echo "....Code Clone Successful"
            }
        }
        
        stage("Build"){
             steps{
                 echo "This is building the code"
                 sh "docker build -t notes-app:latest ."
             }
            
        }
        stage("Test"){
             steps{
                     echo "This is Testing the code"
             }
            
        }
        stage("Push to DockerHub"){
             steps{
                     echo "This is Pushing Image to Docker Hub"
                     withCredentials([usernamePassword('credentialsId':"dockerHubCred",
                     passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                     sh "docker login -u  ${env.dockerHubUser} -p  ${env.dockerHubPass} " 
                     sh "docker image tag notes-app:latest ${env.dockerHubUser}/notes-app:latest"
                     sh "docker push ${env.dockerHubUser}/notes-app:latest"
                     }
             }
            
        }
        stage("Deploy"){
             steps{
                     echo "This is  deploying the code"
                    //sh "docker run -d -p 8000:8000 notes-app:latest"
                    
                    sh " docker compose down && docker compose up -d"
             }
            
        }
        
        
    }
}
