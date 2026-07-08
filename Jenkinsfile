pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                bat 'dotnet build'
            }
        }
        stage('Tests') {
            steps {
                bat 'dotnet test'
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner for MSBuild'
                    withSonarQubeEnv('SonarQubeServer') {
                        bat "\"${scannerHome}\\SonarScanner.MSBuild.exe\" begin /k:\"smswebapp\""
                        bat "dotnet build"
                        bat "\"${scannerHome}\\SonarScanner.MSBuild.exe\" end"
                    }
                }
            }
        }
    }
}
