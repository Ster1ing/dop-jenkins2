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
          agent any
          options {
            timeout(time: 60, unit: "SECONDS")
          }
          steps {
            script {
              try {
                dir("/home/runner/work/jenkins-task2-Ster1ing/jenkins-task2-Ster1ing/jenkinsHome/workspace/${GLOB_JOB_NAME}/target") {
                  sh "java -jar contact.war"
                }
              } catch (Throwable e) {
                echo "Caught ${e.toString()}"
                currentBuild.result = "SUCCESS"
              }
            }
          }
        }
        stage('Running Test') {
          steps {
            sleep(time: 30, unit: "SECONDS")
            sh 'mvn -B test -Dtest=RestIT'
          }
        }
      }
    }
  }
}
