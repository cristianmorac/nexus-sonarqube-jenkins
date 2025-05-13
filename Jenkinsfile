pipeline {
    agent any

    environment {
        // Usa el nombre del servidor configurado en "Configure System"
        SONARQUBE_SERVER = 'sonarqube'
    }

    tools {
        maven 'maven_3' // Nombre exacto como lo tienes configurado
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

        stage('SonarQube Analysis') {
            steps {
                withCredentials([string(credentialsId: 'sonarqube-token', variable: 'SONAR_TOKEN')]) {
                    sh 'mvn sonar:sonar -Dsonar.login=$SONAR_TOKEN'
                }
            }
    }
}
