pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/roffilortegacoronado-hub/smswebapp.git',
                    credentialsId: 'github-Token'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build'
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONARQUBE = credentials('sonarqube-token')
            }
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    sh 'dotnet sonarscanner begin /k:"smswebapp" /d:sonar.login=$SONARQUBE'
                    sh 'dotnet build'
                    sh 'dotnet sonarscanner end /d:sonar.login=$SONARQUBE'
                }
            }
        }
    }
}
