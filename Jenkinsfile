pipeline {
  agent any
	stages {

		stage('Checking out git repo') {
    	  	steps {
				echo 'Checkout...'
      			checkout scm
			  }			  
    	}	

		stage('Building Capstone Docker Image') {
			steps {
				withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'executive', usernameVariable: 'gemmaddy')]) {
					sh '''
							docker build -t gemmaddy/capstone .
						'''
				}
			}
		}
	}	
}
