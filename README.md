# 🚀 DevOps Infrastructure Project

A complete CI/CD-ready DevOps project using **Docker**, **Kubernetes**, **Ansible**, **Terraform**, and **Jenkins**, deployed on **AWS**.

---

## 🧰 Tech Stack

| Tool        | Purpose                                                                 |
|-------------|-------------------------------------------------------------------------|
| Terraform   | Provision AWS infrastructure (EC2, VPC, optional EKS)                   |
| Ansible     | Configure EC2 instance (install Docker, Jenkins)                        |
| Docker      | Containerize a sample Flask application                                 |
| Kubernetes  | Deploy application to EKS with HPA                                       |
| Jenkins     | Automate CI/CD pipeline: build, push image, deploy to K8s               |

---

## 📁 Project Structure

```bash
devops-infra-project/
├── terraform/          # AWS infra (EC2, VPC, optional EKS)
├── ansible/            # EC2 configuration with Ansible
├── jenkins/            # Jenkins pipeline config
├── app/                # Sample Dockerized Flask App
├── k8s/                # Kubernetes manifests (deployment, service, HPA)
└── README.md           # Project documentation


🛠️ How to Set Up and Run the Project
🔹 Step 1: Clone the Repository

git clone https://github.com/Anwesha-web/devops-infra-project.git
cd devops-infra-project

🔹 Step 2: Provision AWS Infrastructure Using Terraform
This will create an EC2 instance for Jenkins.

cd terraform/
terraform init
terraform apply

✅ Confirm when prompted by typing yes.

🔹 Step 3: Configure EC2 Instance with Ansible
1. Get your EC2 Public IP from the AWS console.

2. Edit the Ansible inventory file:
# ansible/inventory
jenkins ansible_host=<your_ec2_public_ip> ansible_user=ec2-user

3. Run the playbook:

cd ../ansible/
ansible-playbook -i inventory playbook.yml

✅ This installs Docker and Jenkins on the EC2 instance.

🔹 Step 4: Build and Push Docker Image to DockerHub
1. Replace your-dockerhub-username in the command below:

cd ../app/
docker build -t your-dockerhub-username/flask-app:latest .
docker login
docker push your-dockerhub-username/flask-app:latest

✅ This builds and pushes your app container.


🔹 Step 5: Deploy Application to Kubernetes (EKS or Minikube)
Make sure kubectl is connected to your cluster.

cd ../k8s/
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f hpa.yaml

✅ This will deploy the app and configure autoscaling.

🔹 Step 6: Configure Jenkins for CI/CD
Access Jenkins at:
http://<your-ec2-public-ip>:8080

Unlock Jenkins and install suggested plugins.

Create DockerHub credentials in Jenkins:

ID: dockerhub-creds

Username/Password or PAT

Create a Pipeline Job and point to:

Your GitHub repo: https://github.com/Anwesha-web/devops-infra-project.git

Jenkinsfile path: jenkins/Jenkinsfile

✅ The pipeline will:

Clone this repo

Build the Docker image

Push to DockerHub

Deploy to Kubernetes

🔹 Step 7: Access the Application
After deployment, run:

kubectl get svc

Copy the EXTERNAL-IP of the flask-service and open:

http://<external-ip>

You should see:

Hello from DevOps Pipeline!

🎯 Features
🚀 Fully automated infrastructure provisioning

🐳 Dockerized microservice

☸️ Scalable Kubernetes deployment with HPA

🔄 Jenkins CI/CD pipeline

🔐 Secure, modular, and cloud-ready setup


🙋‍♀️ Author
Built with 💻 by Anwesha-web
