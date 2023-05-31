pipeline {
  agent any	
  environment {
    dockerimagename = "azemedkun/react-app"
  }

 
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
          dockerImage = docker.build dockerimagename + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
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