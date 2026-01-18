## Set Of Commands

- **Jenkins Server Setup (AWS, Docker, Kubectl, EKS)**
    - Run as root user
  



````
# Switch to root directory
cd /

# Ensure Jenkins user has bash shell
usermod -s /bin/bash jenkins

# Add Jenkins user to root group (required for docker.sock access)
usermod -G 0 jenkins

# Switch to Jenkins user
su - jenkins

````
- **Verify Java & Maven (Required for Jenkins builds)**

````
# Check Java installation
java -version

# Verify Maven installation
mvn --version


````

- **Install kubectl (Kubernetes CLI)**

````
# Download latest stable kubectl binary
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

# Make kubectl executable
chmod +x kubectl

# Move kubectl to system path
sudo mv kubectl /usr/bin/kubectl

# Verify kubectl installation
kubectl version --client

````

- **Configure Docker Access for Jenkins**
````
# Give Jenkins permission to access Docker socket
sudo chmod 777 /var/run/docker.sock

# Verify Docker access
docker images


````

- **Verify AWS Credentials**
````
# Verify IAM identity
aws sts get-caller-identity



````

- **Connect Jenkins to EKS Cluster**
````
# Update kubeconfig for EKS cluster
aws eks update-kubeconfig \
  --region ap-south-1 \
  --name eks-cluster-fusionfinal

````

- **Verify Kubernetes Access**
````
# Check cluster nodes
kubectl get nodes

# Check running pods
kubectl get pods

# Check services
kubectl get svc


````

- **Description In short**
- **usermod / su** → Ensures Jenkins has a proper shell and required permissions  
- **Java & Maven** → Required for Jenkins build and CI jobs  
- **kubectl** → Allows Jenkins to deploy applications to Kubernetes clusters  
- **Docker socket permission** → Enables Jenkins to run Docker commands and build images  
- **aws configure** → Connects Jenkins to AWS using IAM user credentials  
- **aws sts get-caller-identity** → Confirms the correct IAM user is configured and in use  
- **aws eks update-kubeconfig** → Allows `kubectl` to communicate with the EKS cluster  
- **kubectl get** → Confirms Kubernetes cluster connectivity and resource visibility  
