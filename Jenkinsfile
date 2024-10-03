pipeline {
    agent {
        docker { image 'python:3' }
    }

    environment {
        DOCKER_IMAGE = 'aryanair09/exp6:latest'
    }

    stages {
        stage('Setup Environment') {
            steps {
                def dockerHome = tool 'myDocker'
                env.PATH = "${dockerHome}/bin:${env.PATH}"
                echo 'Setting up Python environment...'
                sh '''
                    if [ -f requirements.txt ]; then
                        pip install -r requirements.txt
                    fi
                '''
            }
        }

        stage('Run Python Script') {
            steps {
                echo 'Running Python script...'
                sh 'python3 script.py'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image...'
                script {
                    sh '''
                        docker build -t $DOCKER_IMAGE .
                    '''
                }
            }
        }

        stage('Docker Login') {
            steps {
                echo 'Logging into Docker Hub...'
                script {
                    sh '''
                        echo "$DOCKERHUB_PASSWORD" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin
                    '''
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Pushing Docker image to Docker Hub...'
                script {
                    sh '''
                        docker push $DOCKER_IMAGE
                    '''
                }
            }
        }

        stage('Post Execution') {
            steps {
                echo 'Cleaning up or generating reports...'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
