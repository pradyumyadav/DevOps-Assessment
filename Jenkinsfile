pipeline {

  environment {
    dockerimagename = "pradyumyadav/nodeapp"
    dockerImage = ""
    registryCredential = 'dockerhublogin'
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/pradyumyadav/DevOps-Assessment.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential )
          {
            dockerImage.push("latest")
          }
        }
      }
    }

    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "kubernetes")
        }
      }
    }

  }

}