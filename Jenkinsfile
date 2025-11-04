pipeline {
    agent any
    
    environment {
        DEPLOY_DIR = '/root/overthecam-v2' 
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/SubiHwang/overthecam-v2.git'
            }
        }

        stage('Copy to Deploy Directory') {
            steps {
                sh '''
                    mkdir -p ${DEPLOY_DIR}
                    cp -r ${WORKSPACE}/. ${DEPLOY_DIR}/
                '''
            }
        }
        
        stage('Build') {
            steps {
                dir("${DEPLOY_DIR}") {  
                    sh 'docker compose build'
                }
            }
        }
        
        stage('Deploy') {
            steps {
                dir("${DEPLOY_DIR}") { 
                    sh '''
                        docker compose down
                        docker compose up -d
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo '배포 성공! ⭐️'
        }
        failure {
            echo '배포 실패 ❌'
        }
    }
}