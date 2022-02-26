pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
         bat 'docker build -t conroy3644/capstone-2:latest .'
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          bat 'docker push conroy3644/capstone1-webapp:latest'
         }
      }
    }
	stage('Terraform') {
	  steps {
	    bat 'terraform init'
		bat 'terraform plan'
	  }
	}
	stage('Kubernetes') {
	  steps {
	    bat 'kubectl get all'
	  }
	}
  }
}
