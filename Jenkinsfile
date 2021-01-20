pipeline {
  agent any
  stages {
        stage('DAST') {
          parallel {
            stage('OWASP ZAP') {
              agent any
              steps {
                sh '''
                    #pip install archerysec-cli
                    DATE=`date +%Y-%m-%d`
                    TIME=`date +%H%M%S`
                    PROJECT_NAME=DevSecOps
                    export PROJECT_ID=`archerysec-cli -s ${ARCHERY_HOST} -u ${ARCHERY_USER} -p ${ARCHERY_PASS} --createproject --project_name=${PROJECT_NAME}_${DATE}_${TIME} --project_disc=PROJECT_DISC --project_start=${DATE}  --project_end=${DATE} --project_owner=$USER | tail -n1 | jq '.project_id' | sed -e 's/^"//' -e 's/"$//'`
                    echo "PROJECT ID......" $PROJECT_ID
                    export PROJECT_IDNew="$PROJECT_ID"
                    export SCAN_ID=`archerysec-cli -s ${ARCHERY_HOST} -u ${ARCHERY_USER} -p ${ARCHERY_PASS} --zapscan --target_url=''${TARGET_URL}'' --project_id=''$PROJECT_ID'' | tail -n1 | jq '.scanid' | sed -e 's/^"//' -e 's/"$//'`
                    echo "scan id......" $SCAN_ID
                    pwd
                    python ./archerysec_script.py --scanner=zap_scan --scan_id=$SCAN_ID --username=${ARCHERY_USER} --password=${ARCHERY_PASS} --host=${ARCHERY_HOST} --high=10 --medium=15
                    export job_status=`python ./archerysec_script.py --scanner=zap_scan --scan_id=$SCAN_ID --username=${ARCHERY_USER} --password=${ARCHERY_PASS} --host=${ARCHERY_HOST} --high=10 --medium=15`]
                    echo "job_status......" $job_status
                    if [ -n "$job_status" ]
                    then
                       echo "Build Sucess"
                    else
                        echo "BUILD FAILURE: Other build is unsuccessful or status could not be obtained."
                        exit 100
                    fi
                  '''
                environment {
                  PROJECT_ID_VIN = ${PROJECT_ID}
                }
              }
            }
          }
        }
    }
    
    post {
        always {
          echo 'ProjectID ${PROJECT_ID}'
          script {
            echo "host : ${params.ARCHERY_HOST}"
            echo sh(script: 'env|sort', returnStdout: true)
          }
          /*
            office365ConnectorSend webhookUrl: 'https://ibsoftware12.webhook.office.com/webhookb2/a697780d-8b74-48c9-b566-f1a113048edb@4fb49922-20aa-49cd-b53a-e7eedbd903b0/JenkinsCI/b1b550a29c3c4b28a3f3ab2c799c520c/b6b23246-1666-4c0e-9f9a-94036cfe6d9e',
            message: 'Result has been available in $params.ARCHERY_HOST/proj_data/?project_id=$params.SCAN_ID',
            status: 'Success'
            */
        }
    }
    
}
