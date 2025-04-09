pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube' // Must match the name in Jenkins > Configure System
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/kp2524/HelloApp.git'
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
