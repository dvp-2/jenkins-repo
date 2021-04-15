pipeline {
    agent any
 stages {
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:8 .' 
                sh 'docker tag nginxtest:8 dvp1/nginx-jenkins:8'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
          withDockerRegistry([ credentialsId: "dockerhubcred", url: "" ]) {
       
          sh  'docker push dvp1/nginx-jenkins:8' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 3001:80 nginxtest:8"
 
            }
        }
 
    }
}
