pipeline{
    agent {label "raw"}
    stages{
        stage("code"){
            steps{
                script{
                    code("https://github.com/Deepak-Pathak1234/django-notes-app.git","main")
                }
              
               
            }
        }
       
        stage("build"){
            steps{
                sh "docker build -t notes-app ."
                echo "building code is done ffff"
            }
        }
       stage('Push Image') {
        steps {
        withCredentials([
            usernamePassword(
                credentialsId: 'dockerhubcred',
                usernameVariable: 'dockerhubuser',
                passwordVariable: 'dockerhubpass'
            )
        ]) {
            sh '''
            echo "$dockerhubpass" | docker login -u "$dockerhubuser" --password-stdin
            docker tag notes-app:latest $dockerhubuser/notes-app:latest
            docker push $dockerhubuser/notes-app:latest
            '''
        }
    }
}
        
        stage("compose"){
            steps{
                sh "docker compose down"
                sh "docker compose up -d"
                echo "comopsed up"
            }
        }
    }
}
