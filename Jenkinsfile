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
          sh """
          sudo cat /var/log/apache2/access.log >> apacheErrors
          """
          def errorsFile = './apacheErrors'
          def logContent = readFile(file: apacheErrors)
          def errors = logContent.strip('\n')

          for (String error : errors) {
            if (error =~ /.* (4[0-9][0-9]|5[0-9][0-9]) .*/) {
              echo error
            }
          }
          echo "====== Read ERRORS FINISHED ======"
        }
      }
    }
  }
}
