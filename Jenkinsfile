pipeline {
	agent any
	stages {

		stage('Provisioning kubernetes cluster') {
			steps {
				withAWS(region:'eu-west-1', credentials:'maheshk23') {
					sh '''
						eksctl create cluster \
						--name Dev \
						--version 1.16 \
						--nodegroup-name standard-workers \
						--node-type t2.micro \
						--nodes 2 \
						--nodes-min 1 \
						--nodes-max 3 \
						--node-ami auto \
						--region eu-west-1 \
						--zones eu-west-1a \
						--zones eu-west-1b \
						--zones eu-west-1c \
					'''
				}
			}
		}



		stage('Create config file') {
			steps {
				withAWS(region:'eu-west-1', credentials:'maheshk23') {
					sh '''
						aws eks --region eu-west-1 update-kubeconfig --name Dev
					'''
				}
			}
		}

	}
}
