pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java21'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
pipeline {
    agent any

    tools {
        maven 'Maven'
        jdk 'Java21'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [
                    tomcat9(
                        credentialsId: 'tomcat-credentials',
                        path: '',
                        url: 'http://172.31.23.139:8080'
                    )
                ],
                contextPath: 'myapp',
                war: 'target/*.war'
            }
        }
    }
}
