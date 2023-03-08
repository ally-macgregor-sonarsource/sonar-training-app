pipeline {
  agent any
  stages {
    stage('SonarQube analysis') {
      steps {
        withSonarQubeEnv('SonarQube Localhost') {
          script {
            def scannerHome = tool 'C:/scanners/sonar-scanner-4.7.0.2747-windows';
            def nodeHome = tool 'C:/Program Files/nodejs';
            bat "${scannerHome}/bin/sonar-scanner -Dsonar.nodejs.executable=${nodeHome}/node -X"
          }
        }
      }
    }
    stage("Quality Gate") {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
          // true = set pipeline to UNSTABLE, false = don't
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
