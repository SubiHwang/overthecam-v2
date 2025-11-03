pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', 
                    url: 'https://github.com/SubiHwang/overthecam-v2.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'docker compose build'
            }
        }
        
        stage('Deploy') {
            steps {
                sh '''
                    docker compose down
                    docker compose -p overthecam-v2 up -d
                '''
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