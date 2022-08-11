pipeline {
  agent { 
    label 'slave' 
  }
  tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
  }
  stages {
   stage ('Maven Build') {
      steps {
        script {
          mvn= tool (name: 'Maven', type: 'maven') + '/bin/mvn'
        }
        sh "${mvn} clean install"
      }
    }
  }
}
