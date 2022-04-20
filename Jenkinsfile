pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                echo 'Building'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test') { 
            steps {
                echo 'Testing'
                sh 'npm run test'
            }
        }
        stage('Deploy') { 
            steps {
                echo 'Deploying'
            }
        }
    }

    post {
        failure {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'dwiola123@gmail.com',
                subject: "Build failed in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
        success {
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                to: 'dwiola123@gmail.com',
                subject: "Successful build in Jenkins ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
        }
    }
}