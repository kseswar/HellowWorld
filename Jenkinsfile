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
				 app = docker.build('hellodocker')
				 app.inside{
					sh 'echo $(/usr/bin/curl localhost:8888)'
				 }
				}
	        }
	   }
	   stage('Run Image') {
	        steps {
	        sh 'docker run -d -p 5000:5000 --name hellodocker hellodocker'
	        }
	   }
	   
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
	   
	   stage('Push Docker image') {
	        steps {
		sh 'withCredentials([string(credentialsId: 'dockerHubaccount', variable: 'dockerHubaccount')]){
		sh 'docker login -u payalsasmal -p ${dockerhubaccount}'
		}
		script {
			 app.push("${env.BUILD_NUMBER}")
			 app.push("latest")
			}
		   }	   
	        }
	   
	   }
    }
}
