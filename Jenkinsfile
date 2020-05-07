pipeline {
    environment {
    registry = "payalsasmal/1strepository"
    registryCredential = 'DockerHub'
	}
	agent any
	    stages {
	        stage('Clone Repository') {
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build Docker Image') {
	        steps {
				script {
				 app = docker.build('hellodocker')
				 app.inside {
					sh 'echo $(curl localhost:8888)'
				 }
				}
	        }
	   }
	   stage('Run Image') {
	        steps {
	        sh 'docker run -d -p 5000:5000 --name hellodocker hellodocker'
	        }
	   }
	   
	   stage('Testing') {
	        steps {
	            echo 'Testing..'
	            }
	   }
	   
	   stage('Push Docker image') {
	        steps {
                   script {
		      docker.withRegistry('registry', registryCredential) {
			     app.push("${env.BUILD_NUMBER}")
			     app.push("latest")
			   }
			}	   
	        }
	   
	   }
    }
}
