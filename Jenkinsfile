pipeline{
    agent any;
    stages{
        stage("code clone"){
            steps{
               git url:"https://github.com/sha620/two-tier-flask-app.git",branch:"master" 
            }
        }
        stage("code bild"){
            steps{
                sh "docker build -t app:la ."
            }
        }
        stage("code test"){
            steps{
                echo "test"
            }
            
        }
        stage("push to the docker hub"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"Dockerhubcred",
                passwordVariable:"dockerhubpass",
                usernameVariable:"dockerhubuser"
                )]){
                sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
                sh "docker image tag app:la ${env.dockerhubuser}/app.la"
                sh "docker push ${env.dockerhubuser}/app.la"
                }

                }
        }
        stage("code deploy"){
            steps{
                sh "docker compose up -d --build flask-app"
            }
            
        }
    }
}
