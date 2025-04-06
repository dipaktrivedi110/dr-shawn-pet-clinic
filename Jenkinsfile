pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/dipaktrivedi110/dr-shawn-pet-clinic.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t dr-shawn-clinic .'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing skipped for now'
            }
        }

        stage('Deploy to EC2') {
            steps {
                sh '''
                echo "Deploying to EC2..."
                scp -i /path/to/key.pem Dockerfile app.py requirements.txt ec2-user@your-ec2-ip:/home/ec2-user/dr-shawn/
                ssh -i /path/to/key.pem ec2-user@your-ec2-ip '
                    cd /home/ec2-user/dr-shawn &&
                    docker stop dr-shawn-clinic || true &&
                    docker rm dr-shawn-clinic || true &&
                    docker build -t dr-shawn-clinic . &&
                    docker run -d -p 5000:5000 --name dr-shawn-clinic dr-shawn-clinic
                '
                '''
            }
        }
    }
}
