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
                terraform plan -var='env=${params.env}' -var='region=${params.region}' -out=tfplan_out
                """
            }
        }

        stage('Approval') {
            when {
                expression {
                    return !params.autoApprove
                }
            }
            steps {
                input message: 'Do you want to apply the Terraform plan?', submitter: 'admin'
            }
        }

        stage('Apply') {
            steps {
                sh """
                cd infra
                terraform apply tfplan_out
                """
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'infra/tfplan_out'
        }
    }
}
