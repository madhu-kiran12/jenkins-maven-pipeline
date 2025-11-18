pipeline {
    agent any

    tools {
        maven "Maven-3.9.6"
        jdk "JDK17"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/madhu-kiran12/jenkins-maven-pipeline.git'
            }
        }

        stage('Build') {
            steps {
                echo "Running mvn compile..."
                sh "mvn clean compile"
            }
        }

        stage('Test') {
            steps {
                echo "Running unit tests..."
                sh "mvn test"
            }
        }

        stage('Package') {
            steps {
                echo "Packaging application..."
                sh "mvn package"
            }
        }

        stage('Deploy') {
            steps {
                echo "Simulating deployment..."
                sh "mkdir -p /tmp/deploy"
                sh "cp target/jenkins-maven-pipeline-1.0-SNAPSHOT.jar /tmp/deploy/"
            }
        }
    }

    post {
        success {
            echo "Build and Deployment Successful!"
        }
        failure {
            echo "Build failed!"
        }
    }
}

