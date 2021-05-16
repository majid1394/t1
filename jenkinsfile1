pipeline {
    agent any
	
    tools {
    maven 'maven3'
}
    environment {
     DOCKER_IMAGE='yourImageName:tagName'
}

stages {
	stage('checkout from github') {
	step{
	checkout scm
	}
	}
	stage('Package') {
         	step{
	sh 'mvn clean package -DskipTests'
	checkout scm
	}
	}
	stage('create Docker Image') {
	step{
		script {
		docker_image=docker.build("${env.DOCKER_IMAGE}",'-f./Dockerfile.')
		}
    	}
	}	
 
        stage('Run application container') {
            steps {
                sh "docker run -d -p 8888:8080 --name myAapp ${DOCKER_IMAGE}"
            }
        }
    }
}