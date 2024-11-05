pipeline {
    agent { label 'frontend-node-label' }  // Replace with the actual label of your frontend node
    
    environment {
        GIT_REPO = 'https://github.com/arunkppkl007/tpv-test.git'  // Public GitHub repository
        GIT_BRANCH = 'main'
        DEPLOYMENT_PATH = '/var/www/html'
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code into the deployment path
                dir("${DEPLOYMENT_PATH}") {
                    git branch: "${GIT_BRANCH}", url: "${GIT_REPO}"
                }
            }
        }
        
        stage('Install Backend Dependencies') {
            steps {
                dir("${DEPLOYMENT_PATH}") {
                    // Install Laravel backend dependencies
                    sh 'composer install --no-interaction --prefer-dist --optimize-autoloader' // Use production options if needed
                }
            }
        }
        
        stage('Run Migrations and Optimize Backend') {
            steps {
                dir("${DEPLOYMENT_PATH}") {
                    // Run migrations and optimize Laravel
                    sh '''
                    php artisan migrate --force
                    php artisan optimize:clear
                    php artisan optimize
                    '''
                }
            }
        }
        
        stage('Build Frontend') {
            steps {
                dir("${DEPLOYMENT_PATH}") {
                    // Commands to build the frontend application
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }
        
        stage('Deploy to Frontend Server') {
            steps {
                dir("${DEPLOYMENT_PATH}") {
                    // Deploy frontend artifacts to the frontend server's directory
                    sh 'cp -r build/* /var/www/html/frontend/'  // Replace with the actual frontend deployment path
                }
            }
        }
    }
    
    post {
        success {
            echo 'Deployment completed successfully.'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
