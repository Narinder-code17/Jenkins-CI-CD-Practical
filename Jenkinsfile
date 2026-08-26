pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Checking out source code from GitHub...'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Starting build verification...'

                bat '''
                    if not exist app\\index.html (
                        echo ERROR: Application file not found.
                        exit /b 1
                    )

                    echo Application file found.
                    echo Build completed successfully.
                '''
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'

                bat '''
                    if exist app\\index.html (
                        echo TEST PASSED: Application file exists.
                    ) else (
                        echo TEST FAILED: Application file does not exist.
                        exit /b 1
                    )
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the build logs.'
        }
    }
}