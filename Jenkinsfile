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

        stage('Copy to Deploy Dir') {
            steps {
                sh 'cp -r ${WORKSPACE}/* /root/overthecam-v2/'
            }
        }

        
        stage('Copy to Deploy Directory') {
            steps {
                sh '''
                    mkdir -p ${DEPLOY_DIR}
                    cp -r * ${DEPLOY_DIR}/
                    cp .env ${DEPLOY_DIR}/ 2>/dev/null || true
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
                        docker compose -p overthecam-v2 up -d
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