
pipeline {
    agent any 
    
    stages {
        stage("code") {
            steps {
                echo("pull the code")
                git url: "https://github.com/rajeshkosta/django-notes-app.git", branch: "master"
            }
        }
        
        stage("build") {
            steps {
                echo("build the image")
                sh "docker build -t django ."
            }
        }
        
        stage("push to dockerhub") {
            steps {
                echo("push to dockerhub")
                withCredentials([usernamePassword(credentialsId: 'shivani', usernameVariable: 'shivaniuser', passwordVariable: 'shivanipass')]) {
                    sh "docker tag django ${env.shivaniuser}/django:latest"
                    sh "docker login -u $shivaniuser -p $shivanipass"
                    sh "docker push ${env.shivaniuser}/django:latest"
                }
            }
        }
        
        stage("deploy") {
            steps {
                echo("deployment of image")
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
