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
			parallel(
				Build-Front:{
					sh """
						cd frontend
						npm install
						npm run build 
					"""
				},
				Build-Backend:{
					sh """
						cd backend
						npm install
						npm run build
					"""
				}
			)
			
		}
		stage('Test'){
			agent{
				docker{
					image 'node:13.8.0-stretch-slim'
				}
			}
			steps{
				parallel(
					Test-Frontend:{
						sh """
							cd frontend
							npm build
							npm run test
						"""
					},
					Test-Backend:{
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
