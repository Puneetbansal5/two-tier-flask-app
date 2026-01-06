pipeline{
    
    agent {label "dev"};
    
    stages{
        stage("code clone"){
            steps {
                git url:"https://github.com/Puneetbansal5/two-tier-flask-app.git",branch:"master"
            }
        }
        stage ("build"){
            steps{
                sh "docker build -t two-tier-flask-app ."
            }
        }
        stage("test"){
            steps{
                echo "code is tested here"
                
            }
        }
        stage ("docker hub image push"){
            steps {
                withCredentials([usernamePassword(credentialsId:"dockerhub",
                usernameVariable:"dockerhubuser",
                passwordVariable:"dockerhubpass")]){
                
               sh "docker login -u ${env.dockerhubuser} -p ${env.dockerhubpass}"
               sh "docker image tag two-tier-flask-app ${env.dockerhubuser}/two-tier-flask-app"
               sh "docker push ${env.dockerhubuser}/two-tier-flask-app:latest"
            }
            }
        }
        stage ("Deploy"){
            steps {
                sh "docker compose up -d --build flask-app"
            }
        }
    }
}
