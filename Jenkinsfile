pipeline {
    agent any

    environment {
        BRANCH = ""
    }

    stages {

        stage('Detect Branch') {
            steps {
                script {
                    BRANCH = sh(script: "git rev-parse --abbrev-ref HEAD", returnStdout: true).trim()
                    echo "Detected branch: ${BRANCH}"
                }
            }
        }

        stage('Build') {
            steps {
                echo "Running BUILD stage for ${BRANCH}"
            }
        }

        stage('Test') {
            steps {
                echo "Running TEST stage for ${BRANCH}"
            }
        }

        stage('Prod Deploy') {
            when {
                expression { BRANCH == "master" }
            }
            steps {
                echo "Running PROD DEPLOY (only for master branch)"
            }
        }
    }
}
