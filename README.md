###### This is Max Conroy's repository for the final capstone project for the Per Scholas Cloud DevOps program.

### Goals of this project:
- Use tools like Terraform, kind, vagrant, Cloud Formation, etc (IaC) to provision a Kubernetes environment.
- Create or use an existing Jenkins(CI/CD) pipeline to deploy your Flask application or the app of your choice onto your Kubernetes cluster.
- Install and configure monitoring of your Kubernetes clusters and Flask application.
- Create a load with a tool like slowHTTPtest or stress to simulate application activity. 
- Document and present your progress and results. 

### Components in this pipeline's architecture:
- This GitHub repository
- Jenkins
- Terraform
- Helm
- Docker
- Dockerhub as a container repository
- Amazon Web Services (AWS)
- Amazon Elastic Kubernetes Service (EKS)
- Prometheus and Grafana
- Discord Webhook for Grafana Alerts

### Diagram of pipeline architecture:
![DevOps Diagram](https://user-images.githubusercontent.com/3588520/156100057-f7ae73c8-89b8-415c-9a00-335d8b26baa0.png)

### How the deployment is monitored:
- Prometheus and Grafana are installed on EKS cluster
- Both are proxied for local access
  - <img width="1720" alt="Grafana and Prometheus Configured for Monitoring" src="https://user-images.githubusercontent.com/3588520/156102059-236dcfb8-d116-4bc6-8df5-025ee5140954.png">

- Grafana dashboards 1860 and 8685 are imported for easy monitoring
- 
- Discord webhook is created and added to Grafana
- Alerts are sent to Discord
