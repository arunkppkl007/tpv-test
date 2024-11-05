pipeline {
    agent { label 'TPVclient1' }  // Replace with your frontend node label
    triggers {
        // Automatically triggers the pipeline when there’s a change in GitHub
        pollSCM('* * * * *')  // Checks for changes every minute (adjust as needed)
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Pulls the latest code from GitHub
                checkout scm
            }
        }
        stage('Build Frontend') {
            steps {
                // Commands to build the frontend application
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Deploy to Frontend Server') {
            steps {
                // Commands to deploy build artifacts to the frontend server's directory
                sh 'cp -r build/* /var/www/html/test/'  // Example path; customize as needed
            }
        }
    }
}
