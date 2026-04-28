pipeline {
    agent any

    environment {
        APP_NAME = "my-app"
        DEPLOY_ENV = "production"
    }

    stages {

        stage('Checkout') {
            steps {
                echo '📥 Cloning source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo '🔨 Building project...'
                // Ví dụ:
                sh 'echo Building...'
            }
        }

        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'echo Testing...'
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying ${APP_NAME} to ${DEPLOY_ENV}..."
                sh 'echo Deploying...'
            }
        }
    }

    post {
        always {
            echo '📌 Pipeline finished.'
        }
        success {
            echo '✅ SUCCESS'
        }
        failure {
            echo '❌ FAILED'
        }
    }
}
