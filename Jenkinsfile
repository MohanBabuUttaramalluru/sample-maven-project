pipeline {
    agent any

    environment {
        TOMCAT_URL = 'http://13.49.75.166:8080'
        CRED_ID = 'tomcat-creds'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/<your-username>/<your-repo>.git', branch: 'main'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(credentialsId: "${CRED_ID}", url: "${TOMCAT_URL}")
                ],
                war: '**/target/*.war'
            }
        }
    }

    post {
        success {
            echo '🎉 Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed. Check logs.'
        }
    }
}