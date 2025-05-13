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
    }
}
