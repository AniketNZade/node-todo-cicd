pipeline {
    agent any
    
    stages {
        
        stage("code"){
            steps{
                git url: "https://github.com/AniketNZade/node-todo-cicd.git", branch: "master"
                echo 'Bhaiya code clone hogaya'
            }
        }
        stage("build and test"){
            steps{
                sh "docker build -t nodeapp ."
                echo 'Code build done'
            }
        }
        stage("Push To DockerHub"){
            steps{
                withCredentials([usernamePassword(
                    credentialsId:"471ecc96-c03d-405a-af0d-fa87c98accc6",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
                sh 'echo $dockerHubPass | docker login -u $dockerHubUser --password-stdin'
                sh "docker image tag nodeapp:latest ${env.dockerHubUser}/nodeapp:latest"
                sh "docker push ${env.dockerHubUser}/nodeapp:latest"
                }
            }
        }
         stage("deploy"){
            steps{
                sh "docker-compose down && docker-compose up -d --build"
                echo 'Deployment also done'
            }
        }
    }
}
