pipeline {
  agent any // Defines that the pipeline can run on any available agent

  // Defines the different stages of the pipeline
  stages { 
    
    // First stage to install Apache 2
    stage('Install Apache 2') {

      // Steps to be executed in this stage
      steps {

        // Executes a shell command to install Apache 2
        sh 'sudo apt-get install apache2 -y'
      }
    }

    // Second stage to read Apache log file and check for errors
    stage('Read apache log file and check 400/500 errors') {

      // Steps to be executed in this stage
      steps {

        // Groovy script block for more complex logic
        script {

          // Appends Apache access log to a file named apacheErrors
          sh """
          sudo cat /var/log/apache2/access.log >> apacheErrors
          """
          // Path to the errors file
          def errorsFile = './apacheErrors'
          
          // Reads the content of the errors file
          def logContent = readFile(file: errorsFile)
          
          // Splits the log content by newline
          def errors = logContent.split('\n')

          // Iterates over each line of the log content
          for (String error : errors) {

            // Regex pattern to identify 400/500 errors
            if (error =~ /.* (4[0-9][0-9]|5[0-9][0-9]) .*/) {

              // Prints the error
              echo error
            }
          }

          // Indicates the completion of error reading
          echo "====== Read ERRORS FINISHED ======"
        }
      }
    }
  }
}
