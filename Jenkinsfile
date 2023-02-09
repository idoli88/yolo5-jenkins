pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 700935310038.dkr.ecr.eu-west-2.amazonaws.com
                docker build -t idot-yolo5 .
                docker tag idot-yolo5:latest 700935310038.dkr.ecr.eu-west-2.amazonaws.com/idot-yolo5:latest
                docker push 700935310038.dkr.ecr.eu-west-2.amazonaws.com/idot-yolo5:latest
                '''
            }
        }
    }
}