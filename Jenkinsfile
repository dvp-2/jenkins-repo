pipeline {
    agent any
    stages {
        stage('Example Username/Password') {
            environment {
                richa = credentials('dvp1gitid')
            }
            steps {
                sh 'echo "Service user is $richa_USR"'
                sh 'echo "Service password is $richa_PSW"'
            }
        }
    }
}
