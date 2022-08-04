pipeline{
	agent none
	
	stages{
		stage('Buld'){
			agent{
				docker{
					image 'node:13.8.0-stretch-slim'
				}
			}
			steps{
				parallel(
					FrontendBuild:{
						sh """
							cd frontend
							sh 'ls -a
							npm install
							npm run build
						"""
					},
					BackendBuild:{
						sh""" 
							cd backend
							ls -a
							npm install
							npm run build
						"""
					}
				)
			}
		}
		stage('Test'){
			agent{
				docker{
					image 'node:13.8.0-stretch-slim'
				}
			}
			steps{
				parallel(
					FrontendTest:{
						sh """
							cd frontend
							npm build
							npm run test
						"""
					},
					BackendTest:{
						sh """
							cd backend
							npm build
							npm run test
						"""
					}
				)
			}
		}
	}
}
