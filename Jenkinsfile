pipeline {
    agent any

    environment {
        MY_VAR = 'value'
    }

    options {
        // Optional configuration options
        timeout(time: 1, unit: 'HOURS')
    }

    tools {
        // Define tool versions
        maven 'Maven 3.6.3'
        jdk 'Java 8'
    }

    parameters {
        // Define parameters for the build
        string(name: 'myParam', defaultValue: 'default', description: 'A parameter')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'make'
            }
        }

        stage('Test') {
            parallel {
                stage('Unit Tests') {
                    steps {
                        sh 'make test'
                    }
                }
                stage('Integration Tests') {
                    steps {
                        sh 'make integration-test'
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'scp target/my-app.jar user@server:/path/to/deploy'
            }
        }
    }

    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if the pipeline succeeds'
        }
        failure {
            echo 'This will run only if the pipeline fails'
        }
        unstable {
            echo 'This will run only if the pipeline is marked unstable'
        }
        changed {
            echo 'This will run if the pipeline state has changed from the last run'
        }
    }
}
