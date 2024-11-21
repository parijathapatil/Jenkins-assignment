pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/parijathapatil/Jenkins-assignment'
        TEST_NODE_PATH = '/var/jenkins/Test-Node'
        PROD_NODE_PATH = '/var/jenkins/Prod-Node'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'develop', url: "${GIT_REPO}"
            }
        }

        stage('Test Job') {
            when {
                branch 'develop'
            }
            steps {
                node('Test-Node') {
                    script {
                        // Ensure the workspace is created and files are copied to the Test Node
                        echo "Copying files to Test Node..."
                        sh """
                            mkdir -p ${TEST_NODE_PATH}/workspace/Deploy-Pipeline
                            rm -rf ${TEST_NODE_PATH}/workspace/Deploy-Pipeline/*
                            cp -r * ${TEST_NODE_PATH}/workspace/Deploy-Pipeline/
                        """
                    }
                }
            }
        }

        stage('Prod Job') {
            when {
                branch 'master'
            }
            steps {
                script {
                    // Only run the Prod Job if the Test Job succeeded
                    echo "Running Prod Job..."
                    node('Prod-Node') {
                        sh """
                            rm -rf ${PROD_NODE_PATH}/*
                            cp -r * ${PROD_NODE_PATH}/
                        """
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
