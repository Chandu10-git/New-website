pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo 'Preparing build folder...'
                bat 'if exist build rmdir /s /q build'
                bat 'mkdir build'
                bat 'xcopy "%WORKSPACE%\\*" "%WORKSPACE%\\build\\" /E /I /Y'
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
    }

    post {
        success {
            echo 'Website build successful!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
