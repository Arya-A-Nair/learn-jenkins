pipeline {
    agent any

    stages {
        stage('Setup Environment') {
            steps {
                echo 'Setting up Python environment...'
                // Install Python dependencies using pip if a requirements file exists
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
                // Run your Python program (replace 'script.py' with your filename)
                sh 'python3 script.py run'
            }
        }
         stage('Test Python Script') {
            steps {
                echo 'Running Python script...'
                // Run your Python program (replace 'script.py' with your filename)
                sh 'python3 script.py test'
            }
        }

        stage('Post Execution') {
            steps {
                echo 'Cleaning up or generating reports...'
                // Add any post-execution steps like cleaning or report generation
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
