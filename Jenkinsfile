pipeline {
    // Use any agent
    agent any
    environment {
        // Set the environment variable APP_PORT=9090
        APP_PORT = '9090'
        // Save the job name in a global variable
        GLOB_JOB_NAME = "${env.JOB_NAME}"
    }      
    stages {
        stage('Build') {
            steps {
                // Use the maven package phase to build the project
                sh 'mvn -B package -DskipTests'
            }
        }
        stage('Integration Test') {            
            // Run the following stages in parallel
            parallel {
                stage('Running Application') {
                    // Use any agent
                    agent any
                    // Set 60 seconds to complete the task
                    options {
                        timeout(time: 60, unit: "SECONDS")
                    }
                    steps {
                        // Open the script block
                        script {
                            // Open the try block
                            try {
                                // Use the dir("TODO") { Commands } construct to return to the target folder
                                // Run the "contact.war" application from the "target" folder
                                echo "This is branch TRY"
                            // Open the catch block
                            } catch (Throwable e) {
                                // Return "success" if the task is stopped after 60 seconds
                                echo "Caught ${e.toString()}"
                                currentBuild.result = "SUCCESS" 
                            // End of try-catch block
                            }
                        // End of the script block
                        }
                    }
                }
                stage('Running Test') {
                    steps {
                        // Wait 30 seconds for "contact.war" application to run
                        sleep(time: 30, unit: "SECONDS")
                        // Run only the "RestIT" integration test in the "test" phase of maven
                         echo "This is branch b"
                    }
                }
            // End of parallel stages
            }
        }
        stage('Hello'){
            steps {
                sh "echo ${GLOB_JOB_NAME}"
            }
        }
    }
}
