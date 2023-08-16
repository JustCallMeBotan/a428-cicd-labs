pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh'
            }
        }
        stage('Manual Approval'){
            steps {
                input message: 'Lanjut ke tahap Deploy ? (Tekan "Proceed" untuk melanjutkan)'
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                sleep(time:1,unit:"MINUTES")
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
