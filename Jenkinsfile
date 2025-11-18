pipeline {
    agent any

    environment {
        BRANCH = ""
        IMAGE = "adword-website"
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

        stage('Docker Build') {
            steps {
                script {
                    echo "Building Docker image..."
                    sh """
                    docker build -t ${IMAGE}:${BRANCH} .
                    """
                }
            }
        }

        stage('Prod Deploy') {
            when {
                expression { BRANCH == "master" }
            }
            steps {
                script {
                    echo "Deploying to /var/www/html (Production)"
                    sh """
                    sudo cp -r . /var/www/html/
                    """
                }
            }
        }
    }
}
