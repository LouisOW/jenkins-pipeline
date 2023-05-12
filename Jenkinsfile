pipeline {

    agent any
    environment {
        DIRECTORY_PATH ="directory path"
        TESTING_ENVIRONMENT="testing environment"
        PRODUCTION_ENVIRONMENT="Louis Welch"
    }
    stages {
        stage('Build') {
            steps {
                bat 'yarn install'
                bat 'gradle build'
            }
            post{
                always{
                    mail to: "lwlch3@gmail.com",
                    subject: "build status email",
                    body: "build log attached!"
                }
            }
        }
        stage('Test') {
            steps {
                echo "unit tests"
                echo "integration tests"
            }     
        }
        stage('Code Quality Check') {
            steps {
                echo "check the quality of the code"
            }
        }        
        stage('Deploy') {
            steps {
                echo "deploy the application to a $TESTING_ENVIRONMENT specified by the environment variable"
                
            }        
        }
        stage('Approval') {
            steps {
                sleep 10
                echo "Approval requested and approved!"
            }        
        }
        stage('Deploy to production') {
            steps {
                echo "$PRODUCTION_ENVIRONMENT, Deployment to production started and completed!"
            }
        }
        stage('Generate Report') {
            steps {
                echo "Report"
            }   
        }          
    }
}
