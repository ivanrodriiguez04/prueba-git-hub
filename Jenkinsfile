pipeline {
    agent any
    environment {
        projectName = "dvwa"
    }
stages {
    stage('Sonarqube') {
    environment {
        scannerHome = tool 'sonarqubescanner'
    }
    steps {
        withSonarQubeEnv('sonarqubeserver') {
            sh "${scannerHome}/bin/sonar-scanner \
                 -Dsonar.projectKey=dvwa \
                 -Dsonar.projectName=DVWA 
                 -Dsonar.sources=/var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonarqubescanner
                 -Dsonar.login=$SONAR_AUTH_TOKEN"
        }
        timeout(time: 10, unit: 'MINUTES') {
            waitForQualityGate abortPipeline: false
            }
        }
    }
}
}
