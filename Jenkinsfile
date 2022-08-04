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
						sh 'npm version'
						sh 'cd frontend'
						sh 'npm install'
						sh 'npm run build'
					},
					BackendBuild:{
						sh 'sudo chown -R 995:993 "/.npm"'
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
