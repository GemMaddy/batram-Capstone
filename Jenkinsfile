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

		stage('Push Image To Dockerhub') {
				steps {
					withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'executive', usernameVariable: 'gemmaddy')]) {
						sh '''
							docker login -u gemmaddy -p executive
							docker push gemmaddy/capstone
						'''
					}
				}
			}	

		stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-east-2', credentials:'devopsroot') {
					sh '''
						kubectl config use-context arn:aws:eks:us-east-2:854577269254:cluster/capstonecluster
					'''
				}
			}
		}

		stage('Deploy prod container') {
			steps {
				withAWS(region:'us-east-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./prod-controller.json
					'''
				}
			}
		}		

		stage('Create the service in the cluster, redirect to blue') {
			steps {
				withAWS(region:'us-east-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./prod-service.json
					'''
				}
			}
		}				
	}	
}
