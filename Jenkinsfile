pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube'   // Nom de ton serveur Sonar dans Jenkins
        SONARQUBE_TOKEN = credentials('access-sonar')  // ID de ton credential
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
                        def scannerHome = tool 'SonarScanner' // <- Ici on charge SonarScanner installé dans Jenkins
                        sh """
                            ${scannerHome}/bin/sonar-scanner \   
                            -Dsonar.projectKey=Test \   
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
