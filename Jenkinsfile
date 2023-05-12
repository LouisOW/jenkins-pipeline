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
        stage('Unit and Integration Tests') {
            steps {
                echo 'yarn test'
                bat 'gradle test'
                echo "junit 'build/test-results/**/*.xml'"
            }     
        }
        stage('Code Analysis') {
            steps {
                echo "gradle findBugsMain"
                echo "gradle checkstyleMain"
                bat 'gradle pmdMain'
                echo "check the quality of the code"
            }
        }        
        stage('Security Scan') {
            steps {
                echo "jenkins-plugin-commander --install 'https://plugins.jenkins.io/owasp-dependency-check/'"
                bat 'gradle dependencyCheck'
                echo "deploy the application to a $TESTING_ENVIRONMENT specified by the environment variable"
                
            }        
        }
        stage('Deploy to Staging') {
            steps {
                echo "jenkins-plugin-commander --install 'https://plugins.jenkins.io/aws-elastic-beanstalk/'"
                bat 'aws-elastic-beanstalk deploy --env testing'
            }        
        }
        stage('Integration Tests on Staging') {
            steps {
                echo "jenkins-plugin-commander --install 'https://plugins.jenkins.io/selenium/'"
                bat 'selenium run --env testing'
                
            }
        }
        stage('Deploy to production!') {
            steps {
                echo "jenkins-plugin-commander --install 'https://plugins.jenkins.io/aws-elastic-beanstalk/'"
                bat 'aws-elastic-beanstalk deploy --env production'
                echo "$PRODUCTION_ENVIRONMENT, Deployment to production completed!"
            }   
        }          
    }
}
