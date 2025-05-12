pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    environment {
        SONAR_TOKEN = credentials('sonarqube-token')
        SONAR_HOST_URL = 'http://localhost:9000'
        NEXUS_URL = 'http://localhost:8081/repository/maven-releases/'
        NEXUS_CREDENTIALS_ID = 'nexus-credentials'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/tu-usuario/simple-java-server.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Code Analysis - SonarQube') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar -Dsonar.projectKey=simple-java-server -Dsonar.login=$SONAR_TOKEN'
                }
            }
        }

        stage('Deploy Artifact to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: env.NEXUS_CREDENTIALS_ID, usernameVariable: 'NEXUS_USER', passwordVariable: 'NEXUS_PASS')]) {
                    sh """
                        mvn deploy -DaltDeploymentRepository=nexus::default::${NEXUS_URL} \
                        -Dnexus.username=${NEXUS_USER} -Dnexus.password=${NEXUS_PASS}
                    """
                }
            }
        }
    }
}
