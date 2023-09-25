pipeline {
    agent any    
    environment {
        APP_PORT = '9090'
        GLOB_JOB_NAME = "${env.JOB_NAME}"
    }      
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B package -DskipTests'
            }
        }
        stage('Integration Test') {
            parallel {
                stage('Running Application') {
                    steps {
                         echo "This is branch a"
                    }
                }
                stage('Running Test') {
                    steps {
                         echo "This is branch b"
                    }
                }
            }
        }
        stage('Hello'){
            steps {
                sh "echo ${GLOB_JOB_NAME}"
            }
        }
    }
}
