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
			script {
				def container = docker.build('--file=Dockerfile-configserver --tag=config-server:latest --rm=true .')
        	                
			}
	        }
	
    	}
}
