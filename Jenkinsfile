pipeline {
  agent any
	stages {

		stage('Checking out git repo') {
    	  	steps {
				echo 'Checkout...'
      			checkout scm
			  }			  
    	}

		stage('Build Docker Image') {
				steps {
					docker.withRegistery('http://ec2-18-188-155-50.us-east-2.compute.amazonaws.com:8080/','dockerhub'){
						sh '''
							docker build -t gemmaddy/capstone .
						'''
					}
				}
			}

		stage('Push Image To Dockerhub') {
				steps {
					docker.withRegistery('http://ec2-18-188-155-50.us-east-2.compute.amazonaws.com:8080/','dockerhub'){
						sh '''
							docker login -u gemmaddy -p executive
							docker push gemmaddy/capstone
						'''
					}
				}
			}		
	}
}
