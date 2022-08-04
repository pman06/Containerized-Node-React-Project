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
						sh 'pwd && ls'
						sh 'cd frontend'
						sh 'npm install'
						sh 'npm run build'
					},
					BackendBuild:{
<<<<<<< HEAD
						sh 'cd backend'
=======
						sh 'pwd && ls'
						sh 'cd ../backend'
>>>>>>> 2b23bc85d8c24f4c9f8a9b787b0438eaf1b1078c
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
						sh 'pwd && ls'
						sh 'cd frontend'
						sh 'npm build'
						sh 'npm run test'
					},
					BackendTest:{
						sh 'pwd && ls'
						sh 'cd backend'
						sh 'npm build'
						sh 'npm run test'
					}
				)
			}
		}
	}
}
