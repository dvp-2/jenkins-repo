pipeline {
    agent any
   
 stages {
  stage('Docker Build and Tag') {
           steps {
               script {
                def dockerimage = docker.build("dvp1/nginxtest:9")
               }
           
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
                script {
                withRegistry('https://hub.docker.com','dockerhubcred') {
                //    sh 'docker login -u $username -p $password'
                }
                    sh 'docker push dvp1/nginxtest:9'
                 
                }
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 3002:80 nginxtest:9"
 
            }
        }
 
    }
}
