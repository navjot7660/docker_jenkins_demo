pipeline {
	agent any {
	environment {
		GIT_REPOSITORY_URL = 
'https://github.com/navjot7660/docker_jenkins_demo.git'
	DOCKER_IMAGE_NAME = 'navjot2697/docker_jenkins_demo'
	IMAGE_TAG = '1.0'
}
stages {
	stage('Clone Repository') {
		steps {
			script {
				try {
				git branch: 'main' , url:https://github.com/navjot7660/docker_jenkins_demo.git
				}
				catch (Exception e){
				echo "Failed to clone repository: $(e.message)"
				error "Failed to clone repository"
				}
			}
		}
	}
stage('Build Docker Image') {
	steps {
	script {
		try {
		docker.build("${DOCKER_IMAGE_NAME}:${IMAGE_TAG}")
		}
		catch (Exception e) {
		echo "Failed to build Docker image: ${e.message}"
		echo "Failed to build Docker image"
		}
	}
	}
}
stage('Push to Dockerhub') {
	steps {
		script {
		  try {
			withCredentials([usernamePassword(credentialsId: 'navjot2697', usernameVariable: 'DOCKER_USERNAME' , passwordVariable: 'DOCKER_PASSWORD')]) {
	// Explicit login before push
	sh """
	echo "$DOCKER_PASSWORD" | docker login -u
"$DOCKER_USERNAME" --password-stdin
		docker push ${DOCKER_IMAGE_NAME}:${IMAGE_TAG}
		"""
}
} catch ( Exception e) {
	echo "Failed to push Docker image to registry: ${e.message}'
	error "Failed to push Docker image"
} } } } } } 		