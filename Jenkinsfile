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
  }
}
