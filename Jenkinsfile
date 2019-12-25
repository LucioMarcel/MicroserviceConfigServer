pipeline {
	
    	options {
        	skipStagesAfterUnstable()
    	}
    	stages {
		stage('Build') { 
		agent {
				docker {
					image 'maven:3-alpine' 
					args '-v /root/.m2:/root/.m2' 
				}
		    	}
    	        	steps {
    	        	    sh 'mvn -B -DskipTests clean package' 
    	        	}
		}
		stage('Deliver') {
			agent any

			steps {
				sh 'docker build --file=Dockerfile-configserver --tag=config-server:latest --rm=true .'
        	                sh 'docker volume create --name=config-repo'
        		        sh 'docker run --name=config-server --publish=9090:9090 --volume=config-repo:/var/lib/config-repo config-server:latest'
			}
	        }
	
    	}
}
