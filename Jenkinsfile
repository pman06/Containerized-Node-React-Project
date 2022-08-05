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
					BuildFront: {
						sh """
							cd frontend
							npm install
							npm run build 
						"""
					},
					BuildBackend: {
						sh """
							cd backend
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
					TestFrontend: {
						sh """
							cd frontend
							npm build
							npm run test
						"""
					},
					TestBackend: {
						sh """
							cd backend
							npm build
							npm run test
						"""
					}
				)
			}
		}
		stage(Vuln-Scan){
				agent{
					docker{
						image 'node:13.8.0-stretch-slim'
					}
				}
				steps{
					parallel(
						Scan-Frontend:{
							sh """
								cd frontend
								npm install
								npm audit fix
								npm audit fix --audit-level=critical --force
								npm audit --audit-level=critical
							"""
						},
						Scan-Backend:{
							sh """
								cd backend
								npm install
								npm audit fix
								npm audit fix --audit-level=critical --force
								npm audit --audit-level=critical 
							"""
						}
					)
				}
			}
	}
}
