pipeline {
	agent {
		docker {
			image 'shyam2056/maven-jenkins-agent:latest'
			args '--user root -v /var/run/docker.sock:/var/run/docker.sock' // mount Docker socket to access the host's Docker daemon
		}
	}
	environment {
		MY_BUILD_NUMBER = "${env.BUILD_NUMBER}"
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
				sh "docker build -t spring-boot-demo:v${env.MY_BUILD_NUMBER} ."
			}
		}

		stage('Docker Run') {
			steps {
				// Stop and remove the previous container if it exists
				sh 'docker rm -f spring-boot-demo || true'
				sh "docker run -d -p 80:8080 --name spring-boot-demo spring-boot-demo:v${env.MY_BUILD_NUMBER}"
			}
		}
	}
}