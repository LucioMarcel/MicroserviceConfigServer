pipeline {
	agent any
    	options {
        	skipStagesAfterUnstable()
    	}
    	stages {
		stage('Build') { 
			steps {
			    sh 'mvn -B -DskipTests clean package' 
			}
		}
		stage('Deliver') {
			steps {
				script {
					def container = docker.build("config-server:latest")
				}     
			}	
	        }
    	}
}
