pipeline {
  agent any
  parameters {
    string(name: 'TARGET_URL', defaultValue: 'https://www.example.com/', description: 'Please enter url to scan...')
  }
  stages {
        stage('DAST') {
          parallel {
            stage('OWASP ZAP') {
              agent any
              steps {
                  script {
                      try {
                      sh '''
                      docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-full-scan.py -t $TARGET_URL -g gen.conf -r testreport.html
                      '''
                      }
                      catch (err) {
                          echo err.getMessage()
                          sh 'printenv'
                      }
                  }
              }
            }
          }
        }
    }
    post {
        always {
          script {
              emailext attachmentsPattern: '**/*.html', body: 'Hi', 
                    subject: "${env.TARGET_URL} - Build # ${env.BUILD_NUMBER}", 
                    mimeType: 'text/html',to: "vinilnarayan@gmail.com"
          }
        }
    }
}
