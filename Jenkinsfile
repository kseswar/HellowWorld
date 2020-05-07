pipeline {
	agent any
	    stages {
	        stage('Clone Repository') {
	        /* Cloning the repository to our workspace */
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build Docker Image') {
	        steps {
				script {
				 app = docker.build('payalsasmal/hellodocker')
				 app.inside{
					sh 'echo $(curl localhost:8888)'
				 }
				}
	        }
	   }
	   stage('Run Image') {
	        steps {
	        sh 'docker run -d -p 5000:5000 --name hellodocker payalsasmal/hellodocker:v1'
	        }
	   }
	   
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
	   
	   stage('Push Docker image') {
	        steps {
                script {
				    docker.withRegistry('https://registry.hub.docker.com', 'DockerHub') {
					    app.push("${env.BUILD_NUMBER}")
						app.push("latest")
					}
				}	   
	        }
	   
	   }
    }
}
