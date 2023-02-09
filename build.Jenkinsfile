pipeline {
    agent any

    environment {
        AWS_DEFAULT_REGION = 'eu-west-2'
        REGISTRY = '700935310038.dkr.ecr.eu-west-2.amazonaws.com'
        IMAGE_NAME = 'idot-yolo5'


    }
    stages {
        stage('Build') {
            steps {
                sh '''
                aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin $REGISTRY
                docker build -t $IMAGE_NAME .
                docker tag $IMAGE_NAME:latest $REGISTRY/$IMAGE_NAME
                docker push $REGISTRY/$IMAGE_NAME:latest
                '''
            }
            post {
                always {
                    sh 'docker image prune -a --filter "until=240h" -f'
                }
            }
        stage('Trigger Deploy') {
            steps {
                build job: 'AppDeploy', wait: false, parameters: [
                    string(name: 'YOLO5_IMAGE_URL', value: "<$REGISTRY/$IMAGE_NAME:latest>")
                ]
             }
        }
    }
}