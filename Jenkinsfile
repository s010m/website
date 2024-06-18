pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "ubuntu-apache:latest"
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: "${env.BRANCH_NAME}", url: 'https://github.com/s010m/website.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'cp -r * /var/www/html/'
                    }
                }
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").inside {
                        sh 'service apache2 start'
                        sh 'echo "Application deployed on port 82"'
                    }
                }
            }
        }
    }
}
