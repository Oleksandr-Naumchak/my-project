pipeline {
    agent any

    environment {
        REPO_URL = 'git@github.com:Oleksandr-Naumchak/my-project.git' 
        BRANCH = 'main'
        REMOTE_USER = 'jenkins'
        REMOTE_HOST = '176.100.12.164'  // Change to your VM's IP
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
                    sshCommand remoteUser: "${REMOTE_USER}",
                               remoteHost: "${REMOTE_HOST}",
                               command: '''
                               sudo apt update
                               sudo apt install -y apache2
                               sudo systemctl enable --now apache2
                               '''
                }
            }
        }

        stage('Check Apache Status') {
            steps {
                script {
                    sshCommand remoteUser: "${REMOTE_USER}",
                               remoteHost: "${REMOTE_HOST}",
                               command: "systemctl status apache2"
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    sshCommand remoteUser: "${REMOTE_USER}",
                               remoteHost: "${REMOTE_HOST}",
                               command: '''
                               echo "<h1>Deployed Successfully!</h1>" | sudo tee /var/www/html/index.html
                               sudo systemctl restart apache2
                               '''
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
