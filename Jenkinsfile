pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Preparing build folder...'
                bat '''
                if exist build rmdir /s /q build
                mkdir build
                xcopy * build /E /I /Y
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Testing if index.html exists...'
                bat 'if not exist build\\index.html exit 1'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'build/**', fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Website build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
