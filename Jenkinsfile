pipeline {
  agent { 
    label 'slave' 
  }
  stages {
   stage ('Maven Build') {
      steps {
        sh "mvn clean install"
      }
    }
  }
}
