pipeline {
    agent any

    environment {
        REGISTRY_URL = '700935310038.dkr.ecr.eu-west-2.amazonaws.com'
        IMAGE_NAME = 'idot-yolo5'
    }

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
            post {
               always {
                   sh 'docker image prune -a --filter "until=240h" --force'
               }
            }
        }

        stage('Trigger Deploy') {
            steps {
                build job: 'AppDeploy', wait: false, parameters: [
                    string(name: 'YOLO5_IMAGE_URL', value: "$REGISTRY_URL/$IMAGE_NAME:$BUILD_NUMBER")
                ]
            }
        }
    }
}