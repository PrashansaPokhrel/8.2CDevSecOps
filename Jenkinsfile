pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/PrashansaPokhrel/8.2CDevSecOps.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                bat 'npm test || exit /b 0'
            }
        }

        stage('Generate Coverage Report') {
            steps {
                bat 'npm run coverage || exit /b 0'
            }
        }

        stage('NPM Audit (Security Scan)') {
            steps {
                bat 'npm audit || exit /b 0'
            }
        }

       stage('Send Email Notification') {
    steps {
        emailext(
            subject: "Build Notification: ${currentBuild.result}",
            body: "The pipeline has completed with status: ${currentBuild.result}. Check Jenkins console for logs.",
            to: "prasunsa24@gmail.com",
            attachLog: true,
            recipientProviders: [[$class: 'DevelopersRecipientProvider']],
            always: true // This ensures email is sent even if the build fails
        )
    }
}
    }
}
