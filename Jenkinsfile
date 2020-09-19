pipeline {
  agent any
	stages {

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
	}
}
