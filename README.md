### Maximilian Conroy's repository for the final capstone project in the Per Scholas Cloud DevOps program



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
- Kubernetes Metrics-Server for "kubectl top" command
- Prometheus and Grafana
- Discord Webhook for Grafana Alerts

### Diagram of pipeline architecture:
![DevOps Diagram](https://user-images.githubusercontent.com/3588520/156100057-f7ae73c8-89b8-415c-9a00-335d8b26baa0.png)

### How the deployment is monitored:
- Prometheus and Grafana are installed on EKS cluster
- Both are proxied for local access
<img width="1720" alt="Grafana and Prometheus Configured for Monitoring" src="https://user-images.githubusercontent.com/3588520/156102059-236dcfb8-d116-4bc6-8df5-025ee5140954.png">

- Grafana dashboards 1860 and 8685 are imported for easy monitoring
<img width="1720" alt="Grafana Stress Test" src="https://user-images.githubusercontent.com/3588520/156102187-b75c17eb-068b-43e3-92c2-6113eed6c20e.png">
<img width="1720" alt="Grafana Stress Test 2" src="https://user-images.githubusercontent.com/3588520/156102209-a823731c-5b71-4b47-9f5b-c4fea67587d5.png">

- Discord webhook is created and added to Grafana
- Alerts are sent to Discord
<img width="901" alt="CPU Alert Firing to Discord" src="https://user-images.githubusercontent.com/3588520/156102240-d8497be8-7ab1-4b9a-8c74-07a63f01dcec.png">

### Successful deployment of ASP.NET app on Amazon EKS:
<img width="1265" alt="ASP NET App Deployed on AWS EKS" src="https://user-images.githubusercontent.com/3588520/156102614-27938d24-3fd6-4d3b-a9a3-39d9648a0f00.png">

### Successful deployment of simple Python Flask app on Amazon EKS:
<img width="1123" alt="Flask App Deployed on AWS EKS" src="https://user-images.githubusercontent.com/3588520/156102663-45b17429-6b70-449b-a6c2-5c8bd9c679a1.png">
<img width="1028" alt="Flask App Deployed on AWS EKS 2" src="https://user-images.githubusercontent.com/3588520/156102670-502d2645-9e8f-4969-a19e-b8861e40b596.png">

### Use of Kubernetes Metrics-Server for command line monitoring of nodes and pods:
Using command - kubectl top node node_name
<img width="511" alt="Kubectl Top Showing Stressed CPU and Memory of EKS Nodes" src="https://user-images.githubusercontent.com/3588520/156103001-d22cffdb-063b-459e-85d4-57dba500406b.png">

### Accessing Kubernetes pod terminals to execute CPU stress-test:
Using Linux command - for i in $(seq $(getconf _NPROCESSORS_ONLN)); do yes > /dev/null & done
<img width="813" alt="Stressing Pods Using Linux Yes Command" src="https://user-images.githubusercontent.com/3588520/156103229-83b33891-7a37-42e7-a753-4784f4e74961.png">
