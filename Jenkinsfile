pipeline {
    agent any

    environment {
        // Usa el nombre del servidor configurado en "Configure System"
        SONARQUBE_SERVER = 'sonarqube'
    }

    tools {
        maven 'maven_3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('SonarQube Scan') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh '''
                        sonar-scanner \
                          -Dsonar.token=$SONAR_TOKEN
                    '''
                }
            }
        }
    }
}
