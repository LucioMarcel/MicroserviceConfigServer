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
		sh 'cd /home/lucio'
		sh 'ls'
                sh 'sudo docker build --file=Dockerfile-configserver --tag=config-server:latest --rm=true .'
                sh 'sudo docker volume create --name=config-repo'
                sh 'sudo docker run --name=config-server --publish=9090:9090 --volume=config-repo:/var/lib/config-repo config-server:latest'
            }
        }
	
    }
}
