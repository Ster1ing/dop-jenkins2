pipeline {    
    agent any
    environment {        
        APP_PORT = '9090'
        //APP_PORT = '8080'
        GLOB_JOB_NAME = "${env.JOB_NAME}"
    }      
    stages {
        stage('Build') {
            steps {
                sh 'printenv'
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
                                //dir("/root/.jenkins/workspace/${GLOB_JOB_NAME}/target") {                                    
                                    //sh "jar -xvf contact.war"
                                    sh "java -jar contact.war"
                                }                                                                
                                //sleep(time: 11, unit: "SECONDS")
                            } catch (Throwable e) {                                
                                echo "Caught ${e.toString()}"
                                currentBuild.result = "SUCCESS"                             
                            }                        
                        }
                    }
                }
                stage('Running Test') {
                    steps {
                        /*
                        script {                            
	                        try {
                                sh 'curl -v localhost/0:0:0:0:0:0:0:1:9090'		
	                        } catch (Throwable e) {                                
		                        echo "Caught ${e.toString()}"
		                        currentBuild.result = "SUCCESS"                                
	                        }    
                        }
                        */
                        sleep(time: 30, unit: "SECONDS")                        
                        //sh 'mvn -B test -Dtest=RestIT -X'
                        sh 'mvn -B test -Dtest=RestIT'
                    }
                }            
            }
        }       
    }
}
