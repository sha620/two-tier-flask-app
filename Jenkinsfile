pipeline{
    agent any;
    stages{
        stage("clone"){
          steps{
              git url: "https://github.com/sha620/two-tier-flask-app.git", branch: "master"
          }  
        }
        stage("build"){
            steps{
                sh "docker build -t flask:ll ."
            }
            
        }
        stage("test"){
            steps{
                echo "test"
            }
            
        }
        stage("push"){
            steps{
                withCredentials([usernamePassword(
                credentialsId:"new",
                usernameVariable:"user",
                passwordVariable:"pass"
                )]){
                    sh "docker login -u ${env.user} -p ${env.pass}"
                    sh "docker image tag flask:ll ${env.user}/flask:ll"
                    sh "docker push ${env.user}/flask:ll"
                }
            }
            
        }
        stage("deploy"){
            steps{
                sh "docker compose up -d"
            }
            
        }
    }
}
