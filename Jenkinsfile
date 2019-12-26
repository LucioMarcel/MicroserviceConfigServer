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
					docker.withRegistry('', registryCredential) {

						def customImage = docker.build(registry)

						customImage.push(latest)
					}

				}     
			}	
	        }
    	}
}
