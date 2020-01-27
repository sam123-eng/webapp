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
	        sh 'rm trufflehog || true'
		sh 'docker pull gesellix/trufflehog'
		sh 'docker run -t gesellix/trufflehog --json https://github.com/sam123-eng/webapp.git > trufflehog'
		sh 'cat trufflehog'
	    }
	    }
    stage('build'){
      steps{
        sh 'mvn clean package'
      }
    }
	stage ('Source-Composition-Analysis') {
		steps {
		     sh 'rm owasp-* || true'
		     sh 'wget https://raw.githubusercontent.com/devopssecure/webapp/master/owasp-dependency-check.sh'	
		     sh 'chmod +x owasp-dependency-check.sh'
		     sh 'bash owasp-dependency-check.sh'
		     sh 'cat /var/lib/jenkins/OWASP-Dependency-Check/reports/dependency-check-report.xml'
		}
	}

	stage ('SAST') {
		steps {
		withSonarQubeEnv('sonar') {
			sh 'mvn sonar:sonar'
			sh 'cat target/sonar/report-task.txt'
		       }
		}
	}
	  
    stage('deploy-to-tomcat'){
       steps{
         sshagent(['tomcat']) {
         sh 'scp -o StrictHostKeyChecking=no target/*.war ubuntu@15.206.171.244:/home/ubuntu/prod/apache-tomcat-9.0.30/webapps/'
         }
          
        }
     
    }
      
  }
}
