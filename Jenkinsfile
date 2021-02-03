pipeline {
  agent any
  parameters {
    string(name: 'TARGET_URL', defaultValue: '', description: 'Please enter url to scan...')
  }
  stages {
        stage('DAST') {
          parallel {
            stage('OWASP ZAP') {
              agent any
              steps {
                sh '''
                    docker run -v $(pwd):/zap/wrk/:rw -t owasp/zap2docker-stable zap-full-scan.py \
                                  -t $params.TARGET_URL -g gen.conf -r testreport.html
                  '''
              }
            }
          }
        }
    }
    
    post {
        success {
          script {
            office365ConnectorSend webhookUrl: 'https://ibsoftware12.webhook.office.com/webhookb2/a697780d-8b74-48c9-b566-f1a113048edb@4fb49922-20aa-49cd-b53a-e7eedbd903b0/JenkinsCI/b1b550a29c3c4b28a3f3ab2c799c520c/b6b23246-1666-4c0e-9f9a-94036cfe6d9e',
            message: "<pre>Success<br><a href="file:///Users/vinilnarayan/.jenkins/workspace/docker-New/testreport.html">Report</a></pre>",
            status: 'Success'
          }
        }
        failure {
          script {
            office365ConnectorSend webhookUrl: 'https://ibsoftware12.webhook.office.com/webhookb2/a697780d-8b74-48c9-b566-f1a113048edb@4fb49922-20aa-49cd-b53a-e7eedbd903b0/JenkinsCI/b1b550a29c3c4b28a3f3ab2c799c520c/b6b23246-1666-4c0e-9f9a-94036cfe6d9e',
            message: "<pre>Failure</pre>",
            status: 'Failure'
          }
        }
    }
    
}
