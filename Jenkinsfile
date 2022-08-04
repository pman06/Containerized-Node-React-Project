pipeline{
	agent none
	environment {
        HOME = '.'
    }
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
						sh 'ls -a'
						sh 'npm install'
						sh 'npm run build'
					},
					BackendBuild:{
						sh 'cd backend'
						sh 'ls -a'
						sh 'npm install'
						sh 'npm run build .'
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
