pipeline {
  agent any
  stages {
    stage('Containerize App Using Docker Build') {
      steps {
        bat 'docker build -t conroy3644/capstone-2:latest .'
      }
    }
    stage('Push Docker Image to Dockerhub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          bat 'docker push conroy3644/capstone1-webapp:latest'
        }
      }
    }
	stage('Provision AWS Infrastructure Using Terraform') {
	  steps {
	    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "terraform", accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          bat 'echo $AWS_ACCESS_KEY_ID'
		  bat 'echo $AWS_SECRET_ACCESS_KEY'
		  bat 'terraform init -input=false'
          bat 'terraform plan -out=tfplan -input=false'
		  bat 'terraform apply -input=false tfplan'
		  bat 'aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)'
        }
	  }
	}
	stage('Deploy App to AWS EKS Cluster') {
	  steps {
	  	withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', credentialsId: "terraform", accessKeyVariable: 'AWS_ACCESS_KEY_ID', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
		  bat 'kubectl apply -f kubernetes.yml'
	      bat 'kubectl get all'
		}
	  }
	}
  }
}
