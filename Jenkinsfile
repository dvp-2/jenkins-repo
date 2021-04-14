pipeline {
    agent any
    stages {
        stage('Example') {
            steps { 
                echo 'Hello World'
            }
        }
        stage('AADU') {
            steps {
                echo 'Hii, AAdu'
            }
        }
    }
    post {
        always {
            echo " Hii this is a post action
        }
    }
}
