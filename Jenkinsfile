pipeline {
  agent any
  stages {

    /*stage('Create kubernetes cluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'devopsroot') {
					sh '''
						eksctl create cluster \
						--name capstonecluster \
						--version 1.17 \
						--nodegroup-name standard-workers \
						--node-type t2.small \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region us-east-2 \
						--zones us-east-2a \
						--zones us-east-2b \
						--zones us-east-2c \
					'''
				}
			}
		}

    stage('Create conf file cluster') {
			steps {
				withAWS(region:'us-east-2', credentials:'devopsroot') {
					sh '''
						aws eks --region us-east-2 update-kubeconfig --name capstonecluster
					'''
				}
			}
		} */

	stage('Build Docker Image') {
			steps {
				withCredentials(credentials:'dockerhub'){
					sh '''
						docker build -t gemmaddy/capstone .
					'''
				}
			}
		}

	stage('Push Image To Dockerhub') {
			steps {
				withCredentials(credentials:'dockerhub'){
					sh '''
						docker login -u gemmaddy -p executive
						docker push gemmaddy/capstone
					'''
				}
			}
		}		

    /*stage('Build') {
      steps {
        sh 'echo "Hello World"'
        sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
      }
    }

    stage('Lint HTML') {
      steps {
        sh 'tidy -q -e *.html'
      }
    }*/

  }
}