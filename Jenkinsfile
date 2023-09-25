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
            // Run the following stages in parallel
            parallel {
                stage('Running Application') {                    
                    agent any                    
                    options {
                        timeout(time: 10, unit: "SECONDS")
                    }
                    steps {                        
                        script {                            
                            try {
                                // Use the dir("TODO") { Commands } construct to return to the target folder                                
                                dir('/root/.jenkins/workspace/${GLOB_JOB_NAME}/target') {
                                    // Run the "contact.war" application from the "target" folder
                                    sh 'jar -xvf contact.war'
                                    //echo "This is branch to RUN"
                                }
                                //sleep(time: 11, unit: "SECONDS")
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
                        // Wait 30 seconds for "contact.war" application to run
                        sleep(time: 5, unit: "SECONDS")
                        // Run only the "RestIT" integration test in the "test" phase of maven
                         echo "This is branch b"
                    }
                }            
            }
        }       
    }
}
