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
            mail body: 'Build succed', 
                subject: 'Status of pipeline: ${currentBuild.fullDisplayName} - #${currentBuild.result}',
                to: 'karolkawalec99@gmail.com'
        }
        failure{
            mail body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n ${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                subject: 'Status of pipeline: ${currentBuild.fullDisplayName} - #${currentBuild.result}',
                to: 'karolkawalec99@gmail.com'
        }
    }
}
