pipeline {
    agent any    
    environment {
        APP_PORT = '9090'
        GLOB_JOB_NAME = "${env.JOB_NAME}"
    }  
    // Save the job name in a global variable
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B package -DskipTests'
            }
        }
        stage('Hello'){
            steps {
                sh "echo ${GLOB_JOB_NAME}"
            }
        }
    }
}
