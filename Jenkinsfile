pipeline {
  agent any
  parameters {
    string(name: 'url', defaultValue: '', description: 'Please enter url to scan...')
  }
  stages {

    stage('userInput') {
      steps {
        echo "User entered : ${params.url}"
      }
    }
    stage('outputFolderCreating') {
      steps {
        script {
          def myWorkDir = pwd()
          echo "My current working directory is '${myWorkDir}'"
          def myOutputFolder = myWorkDir + "/outPut"

          if (!fileExists("outPut")) {
            echo 'outPut folder not exist'
            if (isUnix()) {
              echo 'Unix OS'
              sh """
								mkdir -p "outPut"
							"""

            }
            else {
              echo 'Windows OS'
            }

          }
          else {
            echo 'outPut folder exists'
		//sh 'rm *.*'
          }
          try {
            sh "ls -la ${myWorkDir}"
            echo 'Succeeded!'
          }
          catch(err) {
            echo "Failed: ${err}"
          }
        }
      }
    }
    stage('NMAP') {
      steps {

        script {

          if (isUnix()) {
            dir("outPut") {
                if (fileExists('NMAP_Result.txt')) {
                    sh 'rm NMAP_Result.txt'
                }
              
              sh """
    						    nmap --open $params.url -oG NMAP_Result.txt
    					    """
            }
          }
          else {
            echo "Windows cmd"
          }
        }
      }
    }
    stage('ReadHost_Port') {
      steps {
        script {
          if (isUnix()) {
            dir("outPut") {
                if (fileExists('NmapOut.txt')) {
                    sh 'rm NmapOut.txt'
                }
	      
              def myWorkDir = pwd()
              echo "My current working directory is '${myWorkDir}'"
              File file = new File(myWorkDir + "/NmapOut.txt")
              def file1 = new File(myWorkDir + "/NMAP_Result.txt")
              def lines = file1.readLines()
              lines.each {
                String line ->

                if (line.contains("Ports:")) {

                  def host = line.substring((line.indexOf("Host: ")), line.indexOf("(")).replace("Host: ", "").replace(" ", "");
                  def ports = line.substring((line.indexOf("Ports: "))).replace("Ports: ", "");
                  //echo "${host}"
                  //echo "${ports}"
                  String[] portarray = ports.split(",");
                  for (int i = 0; i < portarray.length; i++) {
                    def port = portarray[i].substring(0, portarray[i].indexOf("/open")).replace(" ", "");
                    file << host + ":" + port + "\n"
                  }

                }
              }
            }

          }
          else {
            echo "Windows cmd"

          }
        }
      }
    }
    stage('Httpx') {
      steps {

        script {

          if (isUnix()) {
            dir("outPut") {
                if (fileExists('httpx_Output.txt')) {
                    sh 'rm httpx_Output.txt'
                }
              
              sh """
    						    httpx -l NmapOut.txt -silent -o httpx_Output.txt
    					    """
            }
          }
          else {
            echo "Windows cmd"
          }
        }
      }
    }
    stage('Nikto') {
      steps {

        script {

          if (isUnix()) {
            dir("outPut") {
                if (fileExists('nikto_scan_result.html')) {
                    sh 'rm nikto_scan_result.html'
                }
              
              def myWorkDir = pwd()
              def file1 = new File(myWorkDir + "/httpx_Output.txt")
              def lines = file1.readLines()
              lines.each { String line ->
                echo "${line}"
                sh """
    						    nikto -o nikto_scan_result.html -Format html -h ${line}
    					    """
              }
            }
          }
          else {
            echo "Windows cmd"
          }
        }
      }
    }
  }
}
