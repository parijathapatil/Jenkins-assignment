pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'website-container'
        DOCKER_REGISTRY = 'localhost'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/parijathapatil/Jenkins-assignment.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'master') {
                        echo 'Building and deploying to port 82...'
                        sh 'docker run -d -p 82:80 --name website-container website-container'
                    } else if (env.BRANCH_NAME == 'develop') {
                        echo 'Building only, not deploying...'
                    }
                }
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully."
        }

        failure {
            echo "Pipeline failed."
        }
    }
}
