pipeline {
	agent any
	    stages {
	        stage('Clone Repository') {
	        /* Cloning the repository to our workspace */
	        steps {
	        checkout scm
	        }
	   }
	   stage('Build Image') {
	        steps {
	        sh 'docker build -t helloworld:v1 .'
	        }
	   }
	   stage('Run Image') {
	        steps {
	        sh 'docker run -d -p 5000:5000 --name helloworldpip helloworld:v1'
	        }
	   }
	   stage('Testing'){
	        steps {
	            echo 'Testing..'
	            }
	   }
    }
}