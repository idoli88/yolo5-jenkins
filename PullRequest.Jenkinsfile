pipeline {
    agent any

    stages {
        stage('Unittest') {
            steps {
                echo "testing32"
                sh '''
                pip3 install -r requirements.txt
                python3 -m pytest --junitxml results.xml tests


                '''
                }
            post {
                always {
                    junit allowEmptyResults: true, testResults: 'results.xml'
                }
            }
        }
//        stage('Lint') {
//            steps {
//                echo "linting"
//                sh '''
//                python3 -m pylint *.py
//                '''
//            }
//        }
        stage('Functional test') {
            steps {
                echo "testing"
            }
        }
    }
}