pipeline{
    agent any;
    stages{
        stage(clone){
            steps{
                git url: "https://github.com/sha620/two-tier-flask-app.git",branch: "master"
            }
        }
        stage(build){
            steps{
                sh "docker build -t two:ll ."
            }
        }
        stage(test){
            steps{
                echo "test"
            }
        }
        stage(push){
            steps{
              withCredentials([usernamePassword(
                  credentialsId: "PPP",
                  usernameVariable: "user",
                  passwordVariable: "pass"
                  
                  )]) {
                      sh "docker login -u ${env.user} -p ${env.pass}"
                      sh "docker image tag two:ll ${env.user}/two:ll"
                      sh "docker push ${env.user}/two:ll"
                  }
            }
        }
        stage(deploy){
            steps{
                sh "docker compose up -d"
            }
        }
    }
}
