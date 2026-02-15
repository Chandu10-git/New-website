stage('Build') {
    steps {
        echo 'Preparing build folder...'
        bat '''
        if exist build rmdir /s /q build
        mkdir build
        robocopy . build /E /XD build
        exit 0
        '''
    }
}
