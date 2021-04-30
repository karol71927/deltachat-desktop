pipeline{
    agent any
    stages{
        stage('Build'){
            steps{
                echo 'Building' 
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Test'){
            steps{
                echo 'Testing'
                sh 'npm run test'
            }
        }
    }
    post{
        success{
            emailext attachLog: true,
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}",
                recipientProviders: [developers(), requestor()],
                subject: "Success Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}",
                to: 'karolkawalec99@gmail.com'
            mail body: 'Build succed', 
                subject: 'Status of pipeline: ${currentBuild.fullDisplayName} - #${currentBuild.result}',
                to: 'karolkawalec99@gmail.com'
        }
        failure{
            emailext attachLog: true, body: '', subject: '', to: 'karolkawalec99@gmail.com'
            mail body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n ${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                subject: 'Status of pipeline: ${currentBuild.fullDisplayName} - #${currentBuild.result}',
                to: 'karolkawalec99@gmail.com'
        }
    }
}
