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
            emailext body: 'Build succed', subject: 'Build succeed $PROJECT_NAME - $BUILD_NUMBER' 
        }
        failure{
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n ${BUILD_LOG, maxLines=100, escapeHtml=false}', 
                subject: 'Build succeed $PROJECT_NAME - $BUILD_NUMBER'    
        }
    }
}
