pipeline {
    agent any

    tools {
        // Must match the names you configured in Jenkins > Global Tool Configuration
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
                echo "Running Maven compile..."
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                echo "Running Maven tests..."
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Package') {
            steps {
                echo "Packaging the application..."
                sh 'mvn package'
            }
        }

        stage('Deploy') {
            steps {
                echo "Simulating deploy by copying JAR to /tmp/deploy ..."
                sh '''
                    mkdir -p /tmp/deploy
                    cp target/jenkins-maven-pipeline-1.0-SNAPSHOT.jar /tmp/deploy/
                '''
            }
        }
    }

    post {
        success {
            echo "Build completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}

