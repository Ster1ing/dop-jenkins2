# Task on Jenkins Topic

Here is a Java application that uses Maven as the build system. The goal is to set up Jenkins to automate the build and testing process for this application.
So, write a **Jenkinsfile** in the root of the repository and define there:

- [Build](https://www.baeldung.com/maven-skipping-tests) steps and [unit tests](https://howtodoinjava.com/maven/maven-run-junit-tests/) steps
- Set the [environment variable](https://www.jenkins.io/doc/pipeline/tour/environment/) **APP_PORT=9090** to run the application on port 9090
- Save the [name of the job](https://www.jenkins.io/doc/book/pipeline/jenkinsfile/) in a global [variable](https://naiveskill.com/jenkins-pipeline-define-variable/)
- Create a [build](https://www.baeldung.com/maven-skipping-tests) of the project
- [Run](https://www.baeldung.com/java-run-jar-with-arguments) the application and the integration test in [parallel stages](https://www.jenkins.io/blog/2017/09/25/declarative-1/)
- To launch the application, [return](https://www.baeldung.com/ops/jenkins-pipeline-change-to-another-folder) to the build folder; use a saved variable for this
- [Run only](https://maven.apache.org/surefire/maven-surefire-plugin/examples/single-test.html) the **RestIT** integration test in the **test** phase of maven
- In this task, stop the parallel stages by [timeout](https://e.printstacktrace.blog/how-to-time-out-jenkins-pipeline-stage-and-keep-the-pipeline-running/)
- To successfully complete the process, use the **try {}** **catch {}** [construction](https://e.printstacktrace.blog/how-to-time-out-jenkins-pipeline-stage-and-keep-the-pipeline-running/)

Use the following template for the Jenkinsfile:

```groovy
pipeline {
    // Use any agent
    // Set the environment variable APP_PORT=9090
    // Save the job name in a global variable
    stages {
        stage('Build') {
            steps {
                // Use the maven package phase to build the project
            }
        }
        stage('Integration Test') {
            // Run the following stages in parallel
                stage('Running Application') {
                    // Use any agent
                    // Set 60 seconds to complete the task
                    steps {
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
                        // Wait 30 seconds for "contact.war" application to run
                        // Run only the "RestIT" integration test in the "test" phase of maven
                    }
                }
            // End of parallel stages
        }        
    }
}
```

P.S. You have access to [Jenkins playground](https://killercoda.com/online-marathon/course/Jenkins/Jenkins_playground). Otherwise, make sure you have a functional Jenkins instance configured.

