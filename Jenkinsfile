pipeline {
    agent {
        label 'master'
    }
   
 stages {
  stage('Sonar-qube testing') {
           steps {
              
                withSonarQubeEnv(credentialsId: 'sonar-key') {
                sh 'sonar-scanner' 
                }
              
           
          }
        }
  stage('Docker Build and Tag') {
           steps {
               script {
                def dockerimage = docker.build("dvp1/nginxtest:9")
               }
           
          }
        }
     
  stage('Publish image to Docker Hub') {
          
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhubcred', passwordVariable: 'password', usernameVariable: 'username')]) {
                    sh 'docker login -u $username -p $password'
               // script {
               //     dockerimage.push()
               //}
                }
              
                    sh 'docker push dvp1/nginxtest:9'
                
            }
          }
        
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps {
                sh "docker run -d -p 3002:80 dvp1/nginxtest:9"
 
            }
        }
    // stage('Pull the container') {
    //     agent {
    //         label 'jenkins-node'
    //     }
    //     steps {
    //         ansiblePlaybook become: true, credentialsId: 'ansible-node-root', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'dev.ini', playbook: 'docker-image-ansible.yml'
    //     }
    // }
    // stage('run the container') {
    //     agent {
    //         label 'jenkins-node'
    //     }
    //     steps {
    //        ansiblePlaybook become: true, credentialsId: 'ansible-node-root', disableHostKeyChecking: true, installation: 'Ansible', inventory: 'dev.ini', playbook: 'docker-container-ansible.yml'
    //     }
    // }
    }
}
