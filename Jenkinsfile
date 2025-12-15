pipeline {
    agent {
        node {
            label 'Agent-1'
        }
    }

    // environment {
    //     appVersion = ''
    //     url = '172.31.76.23:8081'
    // }

    options {
        timeout(time: 1, unit: 'HOURS')
        disableConcurrentBuilds()
        ansiColor('xterm')
    }

    parameters {
        string(name: 'version', defaultValue: '1.0.0', description: 'What is Artifact Version?')
        choice(name: 'environment', choices: 'dev', description: 'What is the Environment?')
    }

    stages {
        stage('Print version') {
            steps {
                script {
                    sh """
                     echo "version: ${params.version}"
                    echo "environment: ${params.environment}"
                    """
                }
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
