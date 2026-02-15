pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Preparing build folder...'
                bat '''
                if exist build rmdir /s /q build
                mkdir build
                robocopy . build /E /XD build .git
                exit 0
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Checking index.html exists...'
                bat 'if not exist build\\index.html exit 1'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }

        stage('Deploy Locally') {
            steps {
                echo 'Deploying to local folder...'
                // Change this path to your local web folder
                bat '''
                if exist C:\\websites\\mywebsite rmdir /s /q C:\\websites\\mywebsite
                mkdir C:\\websites\\mywebsite
                robocopy build C:\\websites\\mywebsite /E
                exit 0
                '''
            }
        }
    }

    post {
        success {
            echo 'Website build and local deployment successful!'
        }
        failure {
            echo 'Build or deployment failed!'
        }
    }
}
