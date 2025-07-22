#  VProfile Kubernetes Deployment

This project walks through deploying the **VProfile** web application on a Kubernetes cluster using **kOps** on AWS. It includes everything from backend services like MySQL and RabbitMQ to external access via Ingress.


---

#  What’s Included?

VProfile is a Java-based web app with several dependencies, all running as containers on Kubernetes:

- **Tomcat** – Serves the app
- **MySQL** – Relational database (persistent volume attached)
- **RabbitMQ** – Message broker
- **Memcached** – Caching layer
- **NGINX Ingress Controller** – For routing traffic
- **Secrets & PVCs** – For security and persistence

---

##  Tech Stack

- Kubernetes (via **kOps**)
- AWS EC2 + EBS
- Docker
- NGINX Ingress
- Kubernetes Secrets
- Persistent Volumes

---

##  File Overview

App-Deployment-on-K8s-Cluster/
├── appdeploy.yaml         # App (Tomcat) deployment
├── appingress.yaml        # Ingress config
├── appservice.yaml        # Service for app
├── dbdeploy.yaml          # MySQL deployment
├── dbpvc.yaml             # MySQL persistent volume claim
├── dbservice.yaml         # MySQL service (uses port 33066)
├── mcdep.yaml             # Memcached deployment
├── mcservice.yaml         # Memcached service
├── rmqdeploy.yaml         # RabbitMQ deployment
├── rmqservice.yaml        # RabbitMQ service
├── secret.yaml            # Encoded credentials for MySQL and RabbitMQ

---

How to Deploy

Step 1 
Set up the Cluster

Use kOps to spin up the Kubernetes cluster on AWS:

kops create cluster --name=mycluster.k8s.local --zones=us-east-2a --state=s3://<your-s3-bucket>
kops update cluster --yes

Step 2 
Deploy the app 

Apply the Kubernetes Configs

kubectl apply -f 

Step 3 
Verify

kubectl get pods
kubectl get svc 
kubectl get ingress

Step 4
Make a Domain so you can Configure DNS 

Step 5
Configure DNS 

update your DNS with a CNAME Pointing your domain to the NGINX ingress ALB

Step 6 
Visit the app: 

http://<yourdomain>

---

TroubleShooting

Pod Problems: kubectl logs <pod-name>
Test connectivity: kubectl run testbox --rm -it --image=busybox -- /bin/sh
wget -O- vprodb:33066






