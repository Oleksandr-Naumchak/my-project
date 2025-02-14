pipeline {
    agent any

    environment {
        REPO_URL = 'https://github.com/Oleksandr-Naumchak/my-project.git' 
        BRANCH = 'master'
        REMOTE_USER = 'jenkins'
        REMOTE_HOST = '1c-dev01.ajax.local'  // Change to your VM's IP
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH}", url: "${REPO_URL}"
            }
        }

        stage('Install Apache2 on Remote Server') {
            steps {
                script {
                    echo "Install Apache2 on Remote Server"
                }
            }
        }

        stage('Check Apache Status') {
            steps {
                script {
                    echo "Check Apache Status"
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    echo "Deploy Application"
                }
            }
        }
    }

    post {
        success {
            echo "✅ Deployment Successful!"
        }
        failure {
            echo "❌ Deployment Failed!"
        }
    }
}
