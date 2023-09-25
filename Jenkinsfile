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
            options {
                timeout(time: 60, unit: "SECONDS")
            }
            parallel {
                stage('Running Application') {
                    steps {
                        script {
                            try {
                                echo "This is branch TRY"
                            } catch (Throwable e) {
                                echo "Caught ${e.toString()}"
                                currentBuild.result = "SUCCESS" 
                            }
                        }
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
