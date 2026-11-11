
pipeline {
    agent any

    stages {
        stage('SCM Synchronization') {
            steps {
                echo 'Pulling latest code...'
                checkout scm
            }
        }

        stage('Static Verification') {
            steps {
                bat 'mvn validate'
            }
        }

        stage('Compilation & Automated Testing') {
            steps {
                bat 'mvn clean package'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }
    }

    post {
        success {
            echo 'CI Pipeline completed successfully!'
        }
        failure {
            echo 'CI Pipeline failed!'
        }
    }
}
