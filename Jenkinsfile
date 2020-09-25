pipeline {
  agent any
	stages {

		stage('Checking out git repo') {
    	  	steps {
				echo 'Checkout...'
      			checkout scm
			  }			  
    	}	
		
		stage('Lint HTML') {
             		 steps {
               		   sh 'tidy -q -e *.html'
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

		stage('Deploy prod container') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./prod-controller.json
					'''
				}
			}
		}		

		stage('Create the service in the cluster') {
			steps {
				withAWS(region:'us-west-2', credentials:'devopsroot') {
					sh '''
						kubectl apply -f ./prod-service.json
					'''
				}
			}
		}				
	}	
}
