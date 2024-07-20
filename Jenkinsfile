pipeline {
    agent { label 'docker' }
    environment {
        GITHUB_REPO = 'https://github.com/s010m/website'
    }
    stages {
        stage('Clone Repository') {
            steps {
                git url: GITHUB_REPO, branch: 'master'
            }
        }
        stage('Build') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y apache2'
                sh 'cp -r * /var/www/html/'
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                sh 'systemctl restart apache2'
            }
        }
    }
    triggers {
        pollSCM('H/5 * * * *')
    }
}
