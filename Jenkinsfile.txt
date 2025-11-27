pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Build') {
            steps {
                echo "===== BUILD STAGE ====="
                sh 'javac src/Main.java'
                echo "Build completed successfully."
            }
        }

        stage('Test') {
            steps {
                echo "===== TEST STAGE ====="
                sh 'java -cp src Main'
                echo "Test execution completed."
            }
        }

        stage('Package') {
            steps {
                echo "===== PACKAGE STAGE ====="
                sh '''
                    mkdir -p build
                    cd src
                    jar cfe ../build/app.jar Main Main.class
                '''
                echo "Application packaged as build/app.jar"
            }
        }

        stage('Deploy') {
            steps {
                echo "===== DEPLOY STAGE ====="
                sh '''
                    mkdir -p deploy
                    cp build/app.jar deploy/
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
