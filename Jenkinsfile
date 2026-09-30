
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

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    scp -i ~/.ssh/tomcat_deploy \
                        -o StrictHostKeyChecking=no \
                        target/maven-tomcat-app.war \
                        deploy@172.31.23.139:/opt/tomcat/webapps/
              
            }
        }
    }

    post {
        success {
            echo 'Build and deployment completed successfully.'
        }

        failure {
            echo 'Build or deployment failed.'
        }
    }
}
