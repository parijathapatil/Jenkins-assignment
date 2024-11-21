pipeline {
    agent any

    environment {
        GIT_REPO = 'https://github.com/parijathapatil/Jenkins-assignment'
        FOLDER_PATH = '/path/to/your/folder'  // Set the folder where you want to pull the Git content
    }

    stages {
        stage('Pull Git Content') {
            steps {
                script {
                    // Clean up the folder if it exists before pulling fresh content
                    sh """
                    rm -rf ${FOLDER_PATH}/*  // Remove existing content
                    git clone ${GIT_REPO} ${FOLDER_PATH}  // Clone the repository into the specified folder
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Git content pulled successfully to the specified folder.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
