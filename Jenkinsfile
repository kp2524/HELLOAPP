pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube' // Must match what you configured in Jenkins > Configure System
    }

    stages {
        stage('Clone Code') {
            steps {
                git 'https://github.com/kp2524/HELLOAPP.git'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv("${SONARQUBE}") {
                    sh '/opt/homebrew/bin/sonar-scanner'  // 👈 Add full path here
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
