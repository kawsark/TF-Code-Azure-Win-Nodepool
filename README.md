## Step-01: Deploy Terraform Manifests with Nodepool additions (Linux & Windows)
```
# Change Directory
cd TF-Code-Azue-Win-Nodepool/terraform-manifests-aks
 
# Initialize Terraform
terraform init
 
# Validate Terraform manifests
terraform validate
 
# Review the Terraform Plan
terraform plan -out=tfPlan
 
# Deploy Terraform manifests
terraform apply tfPlan
```
 
## Step-02: Verify if Nodepools added successfully
```
# List Node Pools
az aks nodepool list --resource-group terraform-aks-<environment-name> --cluster-name terraform-aks-<environment-name>-cluster --output table
 
# List Nodes using Labels
kubectl get nodes -o wide
```
 

## Step-03: Deploy Sample Applications for all 3 node pools
- Webserver App to System Nodepool
- Dotnet App to Windows Nodepool
```
# Change Directory
cd TF-Code-Azue-Win-Nodepool/

# Deploy All Apps
kubectl apply -R -f kube-manifests/
 
# List Pods
kubectl get pods -o wide
```
 
## Step-04: Access Applications
```
# List Services to get Public IP for each service we deployed
kubectl get svc
 
# Access Webserver App (Running on System Nodepool)
http://<public-ip-of-webserver-app>/app1/index.html
 
# Access Windows App (Running on win101 Nodepool)
http://<public-ip-of-windows-app>
```
 
## Step-05: Destroy our Terraform Cluster
```
# Change Directory
cd TF-Code-Azue-Win-Nodepool/terraform-manifests-aks
 
# Destroy all our Terraform Resources
terraform destroy
```
 
## Step-06: Do yourself a favor – Grab a fine wine & enjoy
```
Go grab a glass of fine wine and enjoy the rest of Friday 😊
