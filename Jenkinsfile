pipeline {
    agent any

    stages {
        stage('Pre') {
            steps {
                sh '''
                curl -L "https://github.com/docker/compose/releases/download/1.29.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
                chmod +x /usr/local/bin/docker-compose
                docker --version
                docker-compose --version
                ls
                '''
                }
        }
        stage('Test') {
            steps {
                sh '''
                echo 'Testing..'
                docker-compose build --no-cache
                '''
                }
        }
       
    }
    
    post {
        
        success {
            echo 'Success!'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                subject: "Success Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                to: 'dwiola123@gmail.com'
         
        }
        
        failure {
            echo 'Failure!'
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                subject: "Failed Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                to: 'dwiola123@gmail.com'
        }
         }
   
}