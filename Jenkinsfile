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
			stage("Test"){
				steps{
					sh 'mvn test'
				}
			}
			stage('Deploy') {
				steps {
					script {
						docker.withRegistry('https://registry.hub.docker.com', registryCredential) {

							def customImage = docker.build(registry+":latest")

							customImage.push()
					Delivery	}

					}     
				}	
			}
		}
	}
