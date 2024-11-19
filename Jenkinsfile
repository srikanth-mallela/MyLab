pipeline {
    // Directives
    agent any

    tools {
        maven 'maven3' // Ensure this matches your Jenkins Maven configuration
    }

    stages {
        // Stage 1: Build
        stage('Build') {
            steps {
                script {
                    echo 'Building the project...'
                    sh 'mvn clean compile package'
                }
            }
        }

        // Stage 2: Testing
        stage('Test') {
            steps {
                script {
                    echo 'Running tests...'
                    sh 'mvn test'
                }
            }
        }

        // Stage 3: Archive Artifacts
        stage('Archive') {
            steps {
                script {
                    echo 'Archiving build artifacts...'
                    archiveArtifacts artifacts: '**/target/*.war', fingerprint: true
                }
            }
        }
    }

    post {
        always {
            script {
                echo 'Cleaning up workspace...'
                cleanWs() // Clean workspace after pipeline execution
            }
        }
        success {
            echo 'Pipeline executed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the logs.'
        }
    }
}
