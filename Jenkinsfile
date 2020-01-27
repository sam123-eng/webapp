pipeline{
  agent any
  tools{
    maven 'Maven'
  }
  stages{
    stage('initialize'){
      steps{
        sh '''
            echo "PATH=${PATH}"
            echo "M2_HOME=${M2_HOME}"
          '''
      }
    }
    stage ('Check-Git-Secrets') {
		    steps {
	        sh 'del /f trufflehog'
		sh 'docker pull gesellix/trufflehog'
		sh 'docker run -t gesellix/trufflehog --json https://github.com/devopssecure/webapp.git > trufflehog'
		sh 'type trufflehog'
	    }
	    }
    stage('build'){
      steps{
        sh 'mvn clean package'
      }
    }
    stage('deploy-to-tomcat'){
       steps{
         sshagent(['tomcat']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@15.206.171.244/home/ubuntu/prod/apache-tomcat-9.0.30/webapps/'
         }
          
        }
     
    }
      
  }
}
