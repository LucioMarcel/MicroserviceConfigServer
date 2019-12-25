pipeline {
	environment {
		registry = "luciomarcel/demo"
    		registryCredential = 'dockerhub'
	}
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
					docker.withRegistry('', registryCredential) {

						def customImage = docker.build("config-server:latest")

						customImage.push()
					}

				}     
			}	
	        }
    	}
}
