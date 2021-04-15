pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:9 .' 
                sh 'docker tag nginxtest:9 dvp1/nginx-jenkins:9'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
                withregistry( '','dockerhubcred' ) {
          sh  'docker push dvp1/nginx-jenkins:9' 
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
