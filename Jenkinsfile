pipeline {
    agent any

    tools {
        maven 'Maven-3.9.16'
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
                deploy(
                    adapters: [
                        tomcat9(
                            alternativeDeploymentContext: '',
                            credentialsId: 'tomcat-credentials',
                            path: '',
                            url: 'http://172.31.23.139:8080'
                        )
                    ],
                    contextPath: null,
                    war: 'target/*.war'
                )
            }
        }
    }
}
