pipeline {
    agent any
    
    triggers {
    	pollSCM('* * * * *')
    }
    
    stages {
        stage('Build') {
            steps{
                sh 'echo "build"'
                sh './gradle build'
                sh 'ls -l build/libs'
            }
        }

        stage('Docker image') {
            steps{
                sh 'echo "image"'
            }
        }

        stage('Deploy to DEV') {
            steps{
                withCredentials([[$class: 'FileBinding', credentialsId: 'kubectl-config-file', variable: 'KUBECTL_CONFIG_FILE']]) {
                    sh 'echo "deploy"'
                }
            }
        }
    }
}