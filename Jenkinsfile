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
				sh """
					cd frontend
					npm install
					npm run build 
					cd ../backend
					npm install
					npm run build
				"""
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
