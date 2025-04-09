pipeline {
    agent any

    tools {
        sonarQubeScanner 'SonarQube' // Must match name in Jenkins config
    }

    environment {
        SONARQUBE = 'SonarQube'
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/your-username/HelloApp.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh 'sonar-scanner'
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}