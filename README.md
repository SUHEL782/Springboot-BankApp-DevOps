#  End-to-End Bank Application Deployment using DevOps on AWS EKS

This project demonstrates a **complete DevOps pipeline** for deploying a multi-tier banking application built using **Spring Boot** on **AWS EKS**.

---

##  Application Preview

![Login](images/login.png)  
![Transactions](images/transactions.png)

---

## 🛠️ Tech Stack

- **Version Control:** GitHub  
- **Containerization:** Docker  
- **CI:** Jenkins  
- **Security:** OWASP Dependency Check  
- **Code Quality:** SonarQube  
- **Vulnerability Scan:** Trivy  
- **CD:** ArgoCD  
- **Container Orchestration:** AWS EKS (Kubernetes)  
- **Monitoring:** Prometheus & Grafana (Helm)  

---

##  Deployment Steps

### 🔹 Pre-requisites

- Root access  
```bash
sudo su

⚠️ This project is deployed in us-west-1 (North California) region.

🔹 Infrastructure Setup

Create EC2 instance (t2.medium, 29GB storage)

Configure Security Groups (required ports)

🔹 AWS & Kubernetes Setup
Install AWS CLI
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
sudo apt install unzip -y
unzip awscliv2.zip
sudo ./aws/install
aws configure
Install kubectl
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/.../kubectl
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin
kubectl version --client
Install eksctl
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version
🔹 Create EKS Cluster
eksctl create cluster --name=bankapp \
  --region=us-west-1 \
  --version=1.30 \
  --without-nodegroup
Associate IAM OIDC
eksctl utils associate-iam-oidc-provider \
  --region us-west-1 \
  --cluster bankapp \
  --approve
Create Node Group
eksctl create nodegroup --cluster=bankapp \
  --region=us-west-1 \
  --name=bankapp \
  --node-type=t2.medium \
  --nodes=2 \
  --node-volume-size=29 \
  --ssh-access \
  --ssh-public-key=eks-nodegroup-key
 Tools Installation
Jenkins
sudo apt update -y
sudo apt install openjdk-17-jre -y
sudo apt install jenkins -y

Change Jenkins port from 8080 → 8081

Docker
sudo apt install docker.io -y
sudo usermod -aG docker ubuntu
SonarQube
docker run -d --name sonar -p 9000:9000 sonarqube:lts-community
Trivy
sudo apt-get install trivy -y
ArgoCD Setup
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

Check pods:

kubectl get pods -n argocd

Expose ArgoCD:

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
 CI/CD Pipeline
Jenkins Pipeline Includes:

Code checkout

Build

SonarQube analysis

OWASP scan

Docker build & push

Trivy scan

Deploy via ArgoCD

 Monitoring Setup
Install Prometheus & Grafana
kubectl create namespace prometheus
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
Expose Services
kubectl edit svc stable-grafana -n prometheus
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
Get Grafana Password
kubectl get secret -n prometheus stable-grafana \
-o jsonpath="{.data.admin-password}" | base64 --decode
 Access Application
http://<worker-node-ip>:30080
 Clean Up
eksctl delete cluster --name=bankapp --region=us-west-1
 Conclusion

This project showcases a complete DevOps lifecycle:

Code → Build → Scan → Containerize → Deploy → Monitor → Automate

⭐ Highlights

End-to-end CI/CD pipeline

Secure & monitored deployment

Kubernetes-based scalable architecture

Production-ready setup

 Author

Suhel Khan
 Uttar Pradesh (Lucknow)
 workwithsuhel@gmail.com

 +91 8931004042
 


---

## ✅ Done

- ✔️ Author moved to bottom  
- ✔️ No content removed  
- ✔️ Clean & structured  
- ✔️ Ready for GitHub + submission  

---

If you want next level 🔥  
I can add:
- ⭐ Architecture diagram (VERY important for shortlist)
- ⭐ CI/CD pipeline flow image
- ⭐ Badges (AWS, Docker, CI/CD status)
