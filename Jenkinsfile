pipeline {
    agent any
    
    environment {
        // Define any environment variables required for the pipeline
        APP_NAME = 'My-React-2'
    }
        stage('Install Dependencies') {
            steps {
                script {
                    sh '''
                        cd my-react-2
                        npm install
                    '''
                }
            }
        }
        
        stage('Build') {
            steps {
                script {
                    sh '''
                        cd my-react-2
                        npm build
                    '''
                }
            }
        }
        
        stage('Test') {
            steps {
                // Run tests (if applicable)
                sh 'echo "test"'
            }
        }
        
        stage('Static Code Analysis - SonarQube') {
            steps {
                script {
                    sh '''
                        echo "Sonar Scanner NOTE : You need to install sonar-scan cli"
                        sonar-scan \
                        -Dsonar.projectKey=CLIENT_PROJECT_KEY \
                        -Dsonar.sources=path:TEST_RESULT \
                        -Dsonar.branch.name=main
                    '''
                }
            }
        }
        
        stage('Deploy') {
            steps {
                script {
                    sh '''
                        echo "Deploy to AWS S3 - you need to install AWS CLI"
                        aws s3 sync YOUR_ARTEFACT_PATH s3://YOUR_S3_BUCKET 
                    '''
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully!'
            // Additional actions or notifications can be added here
        }
        
        failure {
            echo 'Pipeline failed!'
            // Additional actions or notifications can be added here
        }
    }
}
