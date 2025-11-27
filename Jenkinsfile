pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Build') {
            steps {
                echo "===== BUILD STAGE ====="
                bat 'javac src\\Main.java'
                echo "Build completed successfully."
            }
        }

        stage('Test') {
            steps {
                echo "===== TEST STAGE ====="
                bat 'java -cp src Main'
                echo "Test execution completed."
            }
        }

        stage('Package') {
            steps {
                echo "===== PACKAGE STAGE ====="
                bat '''
                if not exist build mkdir build
                cd src
                jar cfe ..\\build\\app.jar Main Main.class
                '''
                echo "Application packaged as build/app.jar"
            }
        }

        stage('Deploy') {
            steps {
                echo "===== DEPLOY STAGE ====="
                bat '''
                if not exist deploy mkdir deploy
                copy build\\app.jar deploy\\app.jar /Y
                '''
                echo "Application deployed (copied) to deploy folder."
            }
        }
    }

    post {
        success {
            echo "PIPELINE SUCCESSFUL!"
        }
        failure {
            echo "PIPELINE FAILED!"
        }
    }
}
