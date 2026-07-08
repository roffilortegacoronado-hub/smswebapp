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
                bat 'dotnet build'
            }
        }
        stage('SonarQube Analysis') {
            environment {
                SONARQUBE = credentials('sonarqube-token')
            }
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    bat 'SonarScanner.MSBuild.exe begin /k:"smswebapp" /d:sonar.login=%SONARQUBE%'
                    bat 'dotnet build'
                    bat 'SonarScanner.MSBuild.exe end /d:sonar.login=%SONARQUBE%'
                }
            }
        }
    }
}
