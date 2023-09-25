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
        stage('Integration Test') {
            // Run the following stages in parallel
                stage('Running Application') {
                    // Use any agent
                    // Set 60 seconds to complete the task
                    steps {
                        sh "echo ${GLOB_JOB_NAME}"
                        // Open the script block
                            // Open the try block
                                // Use the dir("TODO") { Commands } construct to return to the target folder
                                // Run the "contact.war" application from the "target" folder
                            // Open the catch block
                                // Return "success" if the task is stopped after 60 seconds
                            // End of try-catch block
                        // End of the script block
                    }
                }
                stage('Running Test') {
                    steps {
                        sh 'mvn -B test'
                        // Wait 30 seconds for "contact.war" application to run
                        // Run only the "RestIT" integration test in the "test" phase of maven
                    }
                }
            // End of parallel stages
        }        
    }
}
