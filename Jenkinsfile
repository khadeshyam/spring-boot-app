pipeline {
    
    agent {
        docker {
            image 'maven:3.9.0'
            args '-v /root/.m2:/root/.m2 --user root -v /var/run/docker.sock:/var/run/docker.sock'
        }
    }


    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
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