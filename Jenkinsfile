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
              Exception caughtException = null
              catchError(buildResult: 'SUCCESS', stageResult: 'ABORTED') {
                try {
                  dir("${env.JENKINS_HOME}/workspace/${GLOB_JOB_NAME}/target") {                    
                    sh "java -jar contac_t.war"
                    //sleep(time: 61, unit: "SECONDS") /**/
                  }
                } catch (org.jenkinsci.plugins.workflow.steps.FlowInterruptedException e) {
                  echo "Caught ${e.toString()}"
                } catch (Throwable e) {
                  caughtException = e
                }
              }              
              if (caughtException) {
                echo "Caught ERROR ${caughtException.toString()}"
                error caughtException.message
                //currentBuild.result = "FAILURE"
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
