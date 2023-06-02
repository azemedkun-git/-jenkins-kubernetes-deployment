pipeline {
  environment {
    registry = "azemedkun/react-app"
    registryCredential = 'dockerhub-credentials'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Cloning Git') {
      steps {
        git (
				url: 'https://github.com/azemedkun-git/-jenkins-kubernetes-deployment.git',
				branch: 'main',
				changelog: true,
				poll: true
			)
      }
    }
    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
  }
}