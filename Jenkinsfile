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
                            -Dsonar.projectKey=Test \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://localhost:9000 \
                            -Dsonar.token=${SONARQUBE_TOKEN}
                        """
                    }
                }
            }
        }
    }
}
