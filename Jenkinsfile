pipeline{
    agent any
    
    stages{
        
        stage("code"){
            steps{
                echo "cloning the code"
                git url:"https://github.com/rajeshkosta/django-notes-app.git"
            }
            
        }
        stage("build"){
            steps{
                echo "build the image"
                sh "docker build -t jangoimage ."
            }
            
        }
        stage("push docker"){
            steps{
                echo "push to dockerhub"
                withCredentials([usernamePassword(credentialsId:'shivani', usernameVariable:'shivaniuser',passwordVariable:'shivanipass')]){
                    sh "docker tag jangoimage ${env.shivaniuser}/jangoimage:latest" 
                    sh "docker login -u ${env.shivaniuser} -p ${env.shivanipass}"
                    sh "docker push  ${env.shivaniuser}/jangoimage:latest "
                }
            }
            
        }
        stage("run container"){
            steps{
                echo "run the container"
                sh "docker-compose down && docker-compose up -d"
            }
            
        }
    }
}
