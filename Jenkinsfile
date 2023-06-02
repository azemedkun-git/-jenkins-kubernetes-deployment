pipeline {
  	
  environment {
    registry = "azemedkun/react-app"
	registryCredential = "dockerhub-credentials"
    dockerImage = ''
  }
  agent any
  stages {
    stage('Checkout Source') {
      steps {
			git (
				url: 'https://github.com/azemedkun-git/-jenkins-kubernetes-deployment.git',
				branch: 'main',
				changelog: true,
				poll: true
			)
		}
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Pushing Image') {
      steps{
        script {
          docker.withRegistry( 'https://hub.docker.com/', registryCredential ) {
          dockerImage.push("latest")
          }
        }
      }
    }
    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}