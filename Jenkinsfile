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

        stage('Save Logs') {
            steps {
                bat 'type pipeline.log > logs.txt'
            }
        }
    }

    post {
        always {
            emailext(
                subject: "Jenkins Pipeline Notification: ${currentBuild.result}",
                body: """Pipeline execution has completed with status: ${currentBuild.result}.
                Please find the attached logs for more details.""",
                to: "prasunsa24@gmail.com",
                attachmentsPattern: "**/logs.txt"
            )
        }
    }
}
