pipeline {
    agent any 
    tools {
        maven 'Maven3'
    } 
    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub..."
                git url: 'https://github.com/DEV8428/jenkins-demo',
                branch: 'master'
            }
        }

        stage('Build') {
            steps {
                echo "Building the project..."
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh 'mvn test'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                echo "Running SonarQube analysis..."
                // Replace with your SonarQube token
                sh '''
                    mvn sonar:sonar \
                        -Dsonar.projectKey=jenkins-demo \
                        -Dsonar.host.url=http://localhost:9000 \
                        -Dsonar.login=Secret text
                '''
            }
        }

        stage('Archive') {
            steps {
                echo "Archiving artifacts..."
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }
    }

    post {
        success {
            echo '🎉 Build Successful!'
        }
        failure {
            echo '❌ Build Failed!'
        }
    }
}
