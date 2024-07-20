pipeline {
    agent {
        docker {
            image 'ubuntu:latest'
            label 'docker'
        }
    }
    stages {
        stage('Setup') {
            steps {
                sh 'apt-get update'
                sh 'apt-get install -y apache2'
                sh 'apt-get install -y git'
            }
        }
        stage('Build') {
            steps {
                sh 'git clone https://github.com/s010m/website.git'
                sh 'cp -r website/* /var/www/html/'
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
