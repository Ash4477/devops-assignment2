pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/Ash4477/devops-assignment2.git', branch: 'main'
            }
        }

        stage('Clean up containers') {
            steps {
                sh 'docker compose -p game-app down || true'
            }
        }

        stage('Build & Run Containers') {
            steps {
                sh 'docker compose -p game-app -f docker-compose.yml up -d --build'
            }
        }

        stage('Verify Services') {
            steps {
                // Add health checks if needed
                sh 'sleep 10' // Give containers time to start
                sh 'curl -I http://localhost:5050 || true' // Example check
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed. Check logs for details.'
        }
    }
}