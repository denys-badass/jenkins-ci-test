pipeline {
  agent any

  stages {
    stage('Install Apache 2') {
      steps {
        sh 'sudo apt-get install apache2 -y'
      }
    }
    stage('Read apache log file and check 400/500 errors') {
      steps {
        script {
          def logFile = '/var/log/apache2/access.log' // Adjust the path if necessary
          def logContent = readFile(file: logFile).trim()

          if (logContent.contains('~4[0-9][0-9]') || logContent.contains('~5[0-9][0-9]')) {
            error "4xx or 5xx errors found in Apache log"
          } else {
            echo "No 4xx or 5xx errors found in Apache log"
          }
        }
      }
    }
  }
}
