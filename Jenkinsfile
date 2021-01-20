pipeline {
  agent any
  stages {

    stage('userInput') {
      steps {
        echo "User entered : ${TARGET_URL}"
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
	      					echo "TARGET_URL......" $TARGET_URL
						export URL=`${TARGET_URL} | sed 's/https\?:\/\///'`
						echo "URL......" $URL
    						nmap --open $URL -oG NMAP_Result.txt
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
    
    
    }
  }
}
