pipeline {
    agent any  // Run on any available Jenkins agent

    tools {
        maven 'Maven3'  // Name of Maven installation configured in Jenkins
        jdk 'JDK17'     // Name of JDK configured in Jenkins
    }

    stages {
        stage('Checkout') {
            steps {
                echo "Pulling code from GitHub..."
                git branch: 'main', url: 'https://github.com/username/jenkins-demo.git'
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
