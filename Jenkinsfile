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
				withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
					sh '''
							docker build -t gemmaddy/capstone .
						'''
				}
			}
		}

		stage('Push Image To Dockerhub') {
				steps {
					withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
						sh '''
							docker login -u $USERNAME -p $PASSWORD
							docker push gemmaddy/capstone
						'''
					}
				}
			}	

		stage('Set current kubectl context') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl config use-context arn:aws:eks:us-west-2:854577269254:cluster/capstonecluster
					'''
				}
			}
		}
		
		stage('Build image for K8') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {					
						sh '''
							kubectl set image  gemmaddy/capstone
						'''					
					}				
			}
		}	

		stage('Deploy blue container') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./blue-controller.json
					'''
				}
			}
		}

		stage('Deploy green container') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./green-controller.json
					'''
				}
			}
		}			

		stage('Create the service in the cluster, redirect to blue') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./blue-service.json
					'''
				}
			}
		}	

	/*	stage('Wait user approve') {
            steps {
                input "Rredirect to green?"
            }
		}

		stage('Create the service in the cluster, redirect to green') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./green-service.json
					'''
				}
			}
		}*/			
	}	
}
