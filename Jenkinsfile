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
            steps {
                node('Test-Node') {
                    script {
                        // Copy files to the Test Node
                        sh """
                            rm -rf ${TEST_NODE_PATH}/*
                            cp -r * ${TEST_NODE_PATH}/
                        """
                    }
                }
            }
        }

        stage('Prod Job') {
            when {
                branch 'develop'  // Only runs if the develop branch is pushed
            }
            steps {
                script {
                    // Run Prod Job only if Test Job was successful
                    currentBuild.result = 'SUCCESS'
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
