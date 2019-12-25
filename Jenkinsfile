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
					docker.withRegistry('https://https://hub.docker.com', 'dockerhub') {

						def customImage = docker.build("config-server:latest")

						customImage.push()
					}

				}     
			}	
	        }
    	}
}
