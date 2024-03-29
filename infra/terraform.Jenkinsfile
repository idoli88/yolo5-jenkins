pipeline {
    agent any

    parameters {
        string(name: 'env', defaultValue: 'default')
        choice(name: 'region', choices: ['us-east-1', 'us-east-2', 'us-west-1', 'us-west-2', 'eu-central-1', 'eu-west-1', 'eu-west-2', 'eu-west-3', 'eu-north-1'])
        booleanParam(name: 'autoApprove', defaultValue: false)
    }

    stages {
        stage('Plan') {
            steps {
                sh """
                cd infra
                terraform init
                terraform plan -out tfplan_out

                """
            }
        }

        stage('Approval') {
            when {
                expression { params.autoApprove == false }
            }

            steps {
                sh """

                """

            }
        }

        stage('Apply') {
            steps {
                sh """
                cd infra
                terraform apply tfplan_out -auto-approve -var-file=env/${env}.tfvars
                """

            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'tfplan_out'
        }
    }
}