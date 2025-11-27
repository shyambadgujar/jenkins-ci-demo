pipeline {
    agent any

    options {
        timestamps()
    }

    stages {

        stage('Build') {
            steps {
                echo "===== BUILD STAGE (MAVEN CLEAN & COMPILE) ====="
                bat 'mvn clean compile'
                echo "Maven build (compile) completed successfully."
            }
        }

        stage('Test') {
            steps {
                echo "===== TEST STAGE (MAVEN TEST) ====="
                bat 'mvn test'
                echo "Maven tests executed successfully."
            }
        }

        stage('Package') {
            steps {
                echo "===== PACKAGE STAGE (MAVEN PACKAGE) ====="
                bat 'mvn package'
                echo "Maven package completed. JAR created in target/ folder."
            }
        }

        stage('Deploy') {
            steps {
                echo "===== DEPLOY STAGE (COPY JAR TO DEPLOY FOLDER) ====="
                bat '''
                if not exist deploy mkdir deploy
                copy target\\jenkins-ci-demo-1.0-SNAPSHOT.jar deploy\\app.jar /Y
                '''
                echo "Application JAR deployed (copied) to deploy/app.jar"
            }
        }
    }

    post {
        success {
            echo "PIPELINE SUCCESSFUL WITH MAVEN!"
        }
        failure {
            echo "PIPELINE FAILED. Check Maven logs above."
        }
    }
}
