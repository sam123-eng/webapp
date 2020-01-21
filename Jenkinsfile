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
    stage('build'){
      steps{
        bat 'mvn clean package'
      }
    }
    stage('deploy-to-tomcat'){
       steps{
          bat '"C:/Program Files (x86)/WinSCP/WinSCP.exe" -o target/*.war ubuntu@15.206.171.244:8080/home/ubuntu/prod/apache-tomcat-8.5.39/webapps/'
        }
     
    }
      
  }
}
