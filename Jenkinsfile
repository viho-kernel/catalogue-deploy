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
    string(name: 'version', defaultValue: '', description: 'What is the artifact version?')
    string(name: 'environment', defaultValue: 'dev', description: 'What is environment?')
    booleanParam(name: 'Destroy', defaultValue: 'false', description: 'What is Destroy?')
    booleanParam(name: 'Create', defaultValue: 'false', description: 'What is Create?')
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
