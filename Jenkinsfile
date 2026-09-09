pipeline {
    agent any

    environment {
        APP_NAME = 'sample-app'
        DEPLOY_ENV = 'staging'
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code from repository...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Compiling and packaging ${env.APP_NAME}..."
                // Example for Node.js: sh 'npm ci'
                // Example for Java/Maven: sh './mvnw clean compile'
                sh 'echo "Simulating build phase... Compile complete."'
            }
        }

        stage('Test') {
            steps {
                echo 'Executing unit and static analysis test suites...'
                // Example: sh 'npm test' or './mvnw test'
		error("A test failed!")
                sh 'echo "Running test suite... All 42 tests passed."'
            }
        }

        stage('Package') {
            steps {
                echo "Creating release artifact: ${env.APP_NAME}-build-${BUILD_NUMBER}..."
                // Example: sh 'docker build -t myorg/sample-app:${BUILD_NUMBER} .'
                sh 'echo "Artifact packaged successfully."'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying build #${BUILD_NUMBER} to ${env.DEPLOY_ENV} environment..."
                // Example: sh 'kubectl apply -f k8s/staging/'
                sh 'echo "Deployment step completed successfully."'
            }
        }
    }

    post {
        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
        success {
            echo "Build #${BUILD_NUMBER} succeeded! Artifact ready for review."
        }
        failure {
            echo "Build #${BUILD_NUMBER} failed. Sending notification to team..."
        }
    }
}
