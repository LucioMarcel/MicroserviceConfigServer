pipeline {
	environment {
		registry = "luciomarcel/config-server"
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
					docker.withRegistry('https://registry.hub.docker.com', registryCredential) {

						def customImage = docker.build(-t registry)

						customImage.push(latest)
					}

				}     
			}	
	        }
    	}
}
