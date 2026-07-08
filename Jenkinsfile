node {
    stage('SCM') {
        checkout scm
    }

    stage('SonarQube Analysis') {
        def scannerHome = tool 'SonarScanner for MSBuild'
        withSonarQubeEnv('SonarQubeServer') {
            bat "\"${scannerHome}\\SonarScanner.MSBuild.exe\" begin /k:\"smswebapp\""
            bat "dotnet build"
            bat "\"${scannerHome}\\SonarScanner.MSBuild.exe\" end"
        }
    }
}
