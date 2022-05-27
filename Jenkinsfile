pipeline {
    agent any
    environment {
        BUILD_COMPLETE = false
    }
    stages {
        stage('Build') {
            failFast true
            parallel {
                stage('Building') {
                    steps {
                        
                        bat "mvn clean install  > output.log"

                        bat '! grep "WARNING" output.log'

                        script {
                            BUILD_COMPLETE = true
                        }
                    }
                }
                stage('Monitoring the logs') {
                    steps {
                        script {
                            while (BUILD_COMPLETE != true) {
                                bat 'wsl grep "WARNING" output.log'
                            }
                        }
                    }
                }
            }
        }
    }
}
