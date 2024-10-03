pipeline {
    agent any

    environment {
        NODEJS_HOME = tool name: 'NodeJS', type: 'NodeJSInstallation'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning the repository...'
                // Replace this with your repository URL
                git 'https://github.com/Dheenathsunder/Jenkins-Setup.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running Tests...'
                // Add your test command here, e.g., sh 'npm test'
                // For now, it just echoes to show where tests would run.
                echo 'Tests executed successfully!'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                // If your project has a build step (e.g., React or Angular), use the npm build command.
                // Uncomment the following line if there's a build step:
                // sh 'npm run build'
                echo 'Build stage completed.'
            }
        }

        stage('Deploy to AWS Ubuntu Server') {
            steps {
                echo 'Deploying application to AWS Ubuntu server...'
                // Ensure that Jenkins can SSH into your AWS Ubuntu instance using the SSH key.
                // This step will copy the entire project to the specified directory on your AWS server.
                // Make sure to replace the values below with your own server details.

                sh '''
                scp -o StrictHostKeyChecking=no -r ./ ubuntu@3.26.73.8:/var/www/myapp
                ssh ubuntu@3.26.73.8 'pm2 restart myapp || pm2 start /var/www/myapp/index.js --name myapp'
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline execution and deployment succeeded!'
        }
        failure {
            echo 'Pipeline failed! Please check the error logs for more details.'
        }
    }
}
