pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube'                // Nom du serveur dans Jenkins global config
        SONARQUBE_TOKEN = credentials('access-sonar') // ID du credential Jenkins (type: Secret Text)
    }

    stages {
        stage('Checkout SCM') {
            steps {
                checkout scm
            }
        }
       
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE_SERVER}") {
                    script {
                        def scannerHome = tool 'SonarScanner'
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                              -Dsonar.projectKey=Demo \
                              -Dsonar.sources=. \
                              -Dsonar.host.url=http://localhost:9000 \
                              -Dsonar.token=sqp_7daf77d4e07393d6051da4af1a4168fe4a1c539f
                        """
                    }
                }
            }
        }
    }
}
