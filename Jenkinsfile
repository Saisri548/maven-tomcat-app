pipeline {

    agent any

    tools {
        jdk 'Java21'
        maven 'Maven-3.9.16'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Environment') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Build WAR') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Archive WAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.war',
                             fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Maven build completed successfully.'
        }

        failure {
            echo 'Maven build failed.'
        }
    }
}
