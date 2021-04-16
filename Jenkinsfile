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
                withCredentials([usernamePassword(credentialsId: 'dockerhubcred', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'docker login -u $username -p $password'
                    script {
                    docker.dvp1/nginx-jenkins.push('9') 
                    }
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
