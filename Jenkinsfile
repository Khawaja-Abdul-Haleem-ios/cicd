pipeline {
    agent any

    environment {
        PROJECT_NAME = "CICD"
        SCHEME = "CICD"
        DESTINATION = "generic/platform=iOS"
    }

    parameters {
        choice(name: 'TEST_TYPE', choices: ['internal', 'external'], description: 'Choose test distribution type')
    }

    stages {
        stage('Checkout') {
            steps {
                echo "🔄 Checking out branch: ${env.BRANCH_NAME}"
                git credentialsId: '0dae4b11-d489-4f03-a4df-070facbd0a17', url: 'https://github.com/Khawaja-Abdul-Haleem-ios/cicd.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "📦 Installing dependencies (brew, fastlane, etc.)..."
                sh '''
                which brew || (echo "❌ Homebrew not found. Please install it manually.")
                brew install fastlane || true
                '''
            }
        }

        stage('Build & Archive') {
            when {
                branch 'main'
            }
            steps {
                echo "🛠️ Building and archiving the iOS project for ${params.TEST_TYPE} testers..."
                sh "export TEST_TYPE=${params.TEST_TYPE} && fastlane beta"

            }
        }
    }

    post {
        success {
            echo "✅ Build and upload to TestFlight succeeded on ${env.BRANCH_NAME}"
        }
        failure {
            echo "❌ Build or upload failed on ${env.BRANCH_NAME}"
        }
    }
}
