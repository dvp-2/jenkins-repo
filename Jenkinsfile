pipeline {
    agent {
        label 'master'
    }
   
 stages {
  stage('Sonar-qube testing') {
           steps {
              
                withSonarQubeEnv('sonar') {
                sh 'sonar-scanner \    
  -Dsonar.projectKey=sample-key \
  -Dsonar.sources=. \
  -Dsonar.host.url=http://localhost:9000 \
  -Dsonar.login=fd84a454492e936fd6c749089011db4b026d4a33' 
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
