pipeline{
  agent any
  tools{
    maven 'Maven'
  }
  stages{
    stage('initialize'){
      steps{
        bat '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"
          '''
      }
    }
    stage ('Check-Git-Secrets') {
		    steps {
	        bat 'del /f trufflehog'
		bat 'docker pull gesellix/trufflehog'
		bat 'docker run -t gesellix/trufflehog --json https://github.com/devopssecure/webapp.git > trufflehog'
		bat 'type trufflehog'
	    }
	    }
    stage('build'){
      steps{
        bat 'mvn clean package'
      }
    }
    /*stage('deploy-to-tomcat'){
       steps{
         sshagent(['tomcat']) {
         bat '"C:/Program Files (x86)/WinSCP/WinSCP.exe" -o ubuntu@15.206.171.244/home/ubuntu/prod/apache-tomcat-9.0.30/webapps/'
         }
          
        }
     
    }*/
      
  }
}
