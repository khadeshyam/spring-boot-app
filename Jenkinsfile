pipeline {
    
    agent {
        docker {
            image 'maven:3.9.0'
            command 'bash -c "apt-get update && apt-get install -y docker.io && exec \"$@\""'
            args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
        }
    }

    stages {
        stage('Checkout') {
            steps {
                 sh 'echo passed'
            }
        }

        stage('Build') {
            steps {
                sh 'ls -ltr'
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {

                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'ls -ltr'
                sh 'docker build -t spring-boot-demo:latest .'
            }
        }

        stage('Docker Run') {
            steps {
                sh 'docker run -d -p 8080:8080 spring-boot-demo:latest'
            }
        }
    }
}