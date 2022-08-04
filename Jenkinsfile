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
						sh 'cd frontend'
						sh 'npm install'
						sh 'npm run build'
					},
					BackendBuild:{
						sh 'cd backend'
						sh 'npm install'
						sh 'npm run build'
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
						sh 'cd frontend'
						sh 'npm build'
						sh 'npm run test'
					},
					BackendTest:{
						sh 'cd backend'
						sh 'npm build'
						sh 'npm run test'
					}
				)
			}
		}
	}
}