pipeline {
    agent {
        docker {
            image 'maven:3-alpine' 
            args '-v /root/.m2:/root/.m2' 
        }
    }
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Initialize')
	{
	    def dockerHome = 'myDocker'
            env.PATH = "${dockerHome}/bin:${env.PATH}"
	}
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
	stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
	stage('Deliver') {	
            steps {
                sh 'docker build --file=Dockerfile-configserver --tag=config-server:latest --rm=true .'
                sh 'docker volume create --name=config-repo'
                sh 'docker run --name=config-server --publish=9090:9090 --volume=config-repo:/var/lib/config-repo config-server:latest'
            }
        }
	
    }
}
