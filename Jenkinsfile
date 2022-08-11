pipeline {
  agent { 
    label 'slave' 
  }
  tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
  }
  stages {
   stage('Initialize'){
      steps{
          echo "PATH = ${M2_HOME}/bin:${PATH}"
          echo "M2_HOME = /opt/maven"
      }
   }
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
