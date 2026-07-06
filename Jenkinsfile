@Library("shared") _
pipeline{
    agent{label "raw"}
    stages{
        stage("cloning"){
          steps{
              script{
                  code("https://github.com/Deepak-Pathak1234/django-notes-app.git","main")
              }
                
          }
        }
        stage("building"){
            steps{
                echo "building the code"
                sh "docker build -t notes-app ."
            }
        }
        stage("push the code "){
            steps{
                withCredentials([usernamePassword(credentialsId:"dockerhubcred",usernameVariable:"user",passwordVariable:"pass")]){
                echo "pushing the code"
                sh "docker login -u $user -p $pass"
                sh "docker image tag notes-app:latest $user/notes-app:latest"
                sh "docker push $user/notes-app:latest"
                }
            }
        }
        stage("run"){
            steps{
                echo "run the code"
                sh "docker compose down"
                sh "docker compose up"
            }
        }
    }
}
