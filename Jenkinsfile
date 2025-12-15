pipeline {
    agent {
        node {
            label 'Agent-1'
        }
    }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    parameters {

parameters {
    string(name: 'version', defaultValue: '', description: 'Artifact version')
    string(name: 'environment', defaultValue: 'dev', description: 'Environment')
    booleanParam(name: 'Destroy', defaultValue: false, description: 'Destroy infra')
    booleanParam(name: 'Create', defaultValue: false, description: 'Create infra')
}

    }

    stages {
        stage('Print version') {
            steps {
                    sh """
                    echo "version: ${params.version}"
                    echo "environment: ${params.environment}"
                    """
            }
        }

        stage('Init') {
            steps {
                    sh """
                    cd terraform/
                    terraform init --backend-config=${params.environment}/backend.tf -reconfigure
                    """
            }
        }
    }

    post {
        always {
            echo "Pipeline completed."
            deleteDir()
        }

        success {
            echo "Pipeline succeeded!"
        }

        failure {
            echo "Pipeline failed!"
        }
    }
}
