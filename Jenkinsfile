pipeline {
    agent any
 stages {
   stage('Initialize'){
        def dockerHome = tool 'MYDOCKER'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
  stage('Docker Build and Tag') {
           steps {
              
                sh 'docker build -t nginxtest:$BUILD_NUMBER .' 
                sh 'docker tag nginxtest:$BUILD_NUMBER dvp1/nginx-jenkins:$BUILD_NUMBER'
               
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
          withDockerRegistry([ credentialsId: "dockerhubcred", url: "" ]) {
       
          sh  'sudo docker push dvp1/nginx-jenkins:$BUILD_NUMBER' 
        }
                  
          }
        }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "sudo docker run -d -p 4030:80 nginxtest:$BUILD_NUMBER"
 
            }
        }
 
    }
}
