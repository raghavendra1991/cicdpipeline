pipeline {
  agent any
  tools {
      maven 'Maven'
      jdk 'JAVA_HOME'
  }
  stages { 
    stage('CleanUp WorkSpace & Git Checkout') {
      steps {
          // Clean before build
          cleanWs()
          // We need to explicitly checkout from SCM here
          checkout scm
      }
    }
    stage ("Initialize") {
      steps {
          echo "PATH = ${M2_HOME}/bin:${PATH}"
          echo "M2_HOME = /opt/maven"
      }
    }
    stage ("Testing & SonarQube analysis") {
      environment {
	       scannerHome = tool 'SonarQube Scanner'
      }
      steps {
         withSonarQubeEnv('admin') {
            sh "mvn clean verify install sonar:sonar -Dsonar.projectKey=mavenproject \
		 -Dsonar.java.coveragePlugin=jacoco \
                 -Dsonar.jacoco.reportPaths=target/jacoco.exec \
    	         -Dsonar.junit.reportsPaths=target/surefire-reports"
         }
      }
      post {
         success {
            archiveArtifacts artifacts: 'target/*.war' 
         }
      }
    }
    stage('Deploy Atrifacts') {
	  steps {
	      rtUpload (
		 serverId: 'JFrog',
		 spec: '''{
 			"files" :[
			  {
		            "pattern": "target/*.war",
		            "target": "maven/"
	         	  }
		        ]
		 }'''
	     )
	 }
     }	  
  }
}
