pipeline {
    agent {
        docker {
            image '<image-url>'
            args  '--user root -v /var/run/docker.sock:/var/run/docker.sock'
    }
}

    parameters {
        string(name: 'YOLO5_IMAGE_URL', defaultValue: '', description: '')
    }

    stages {
        stage('Deploy') {
            steps {
                sh 'echo $YOLO5_IMAGE_URL'
            }
        }
    }
}