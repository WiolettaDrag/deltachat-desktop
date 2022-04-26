pipeline{
	agent any
	tools{nodejs "NodeJS"}
	stages{
	
	
	stage('Build'){
		steps
		{
			echo 'Building'
			sh 'npm install'
		
		
	}
	post {
		always{
			echo 'Finished'
		}
		success {
			echo 'Success'
			emailext attachLog: true,
				body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				to: 'dwiola123@gmail.com',
				subject: "Build success"
		}
		
		failure {
			echo 'Failure'
			emailext attachLog: true,
				body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				to: 'dwiola123@gmail.com',
				subject: "Build failed."
		}
	
	

	}
}
	
		stage('Test'){
			steps{
				echo 'Testing'
				sh 'npm run test'
		}
		
		post{
	
			always{
				echo 'Finished'
			}
			failure{
				echo 'Failure'
				emailext attachLog: true,
					body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'dwiola123@gmail.com',
					subject: "Test failed"
			}
			success{
				echo 'Success'
				
				emailext attachLog: true,
					body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
					to: 'dwiola123@gmail.com',
					subject: "Test success"
			}
		}	
	}
	
	stage('Deploy') {
            steps {
                echo 'Deploying'
                sh 'docker build -t deploy -f Dockerfile-build .'
                
            }
            post {
                success {
                   echo 'Success'
			emailext attachLog: true,
				body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				to: 'dwiola123@gmail.com',
				subject: "Deploy success"
                }
        
                failure {
                    echo 'Failure'
                    	emailext attachLog: true,
				body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
				to: 'dwiola123@gmail.com',
				subject: "Deploy failed"
                }
            }
        }
	
   }

}
	
