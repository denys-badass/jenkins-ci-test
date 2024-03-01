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
          def errors = []
          sh """
          grep -E '(4|5)[0-9]{2} ' /var/log/apache2/error.log >> errors.txt
          """
          if (fileExists('errors.txt')) {
            errors = readFile('errors.txt').split("\n")
            for (error in errors) {
              echo "Error found: ${error}"
            }
          } else {
            echo 'No 4xx or 5xx errors found in the logs.'
          }
        }
      }
    }
  }
}
