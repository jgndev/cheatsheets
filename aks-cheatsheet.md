---
id: 11
date: 2025-05-02T00:00:00Z
title: AKS Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for AKS (Azure Kubernetes Service)
slug: aks-cheatsheet
tags:
  - azure
  - aks
  - k8s
published: true
---

# Azure Kubernetes Service (AKS) Cheatsheet

---

## Cluster Management

- Create an AKS cluster with basic configuration
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --node-count 3 \
  --enable-addons monitoring \
  --generate-ssh-keys
```

- Create AKS cluster with advanced networking
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --network-plugin azure \
  --vnet-subnet-id <subnet-id> \
  --docker-bridge-address 172.17.0.1/16 \
  --dns-service-ip 10.2.0.10 \
  --service-cidr 10.2.0.0/24
```

- List AKS clusters
```bash
az aks list --output table
```

- Get AKS cluster details
```bash
az aks show --resource-group <resource-group> --name <cluster-name>
```

- Get AKS cluster credentials
```bash
az aks get-credentials --resource-group <resource-group> --name <cluster-name>
```

- Delete AKS cluster
```bash
az aks delete --resource-group <resource-group> --name <cluster-name> --yes --no-wait
```

---

## Node Pool Management

- List node pools
```bash
az aks nodepool list --resource-group <resource-group> --cluster-name <cluster-name>
```

- Add a new node pool
```bash
az aks nodepool add \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --node-count 2 \
  --node-vm-size Standard_DS2_v2
```

- Scale a node pool
```bash
az aks nodepool scale \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --node-count 5
```

- Enable autoscaling for node pool
```bash
az aks nodepool update \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name> \
  --enable-cluster-autoscaler \
  --min-count 1 \
  --max-count 10
```

- Delete a node pool
```bash
az aks nodepool delete \
  --resource-group <resource-group> \
  --cluster-name <cluster-name> \
  --name <nodepool-name>
```

---

## Cluster Operations

- Start stopped AKS cluster
```bash
az aks start --resource-group <resource-group> --name <cluster-name>
```

- Stop AKS cluster
```bash
az aks stop --resource-group <resource-group> --name <cluster-name>
```

- Upgrade AKS cluster
```bash
az aks upgrade \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --kubernetes-version <version>
```

- Get available upgrade versions
```bash
az aks get-upgrades --resource-group <resource-group> --name <cluster-name>
```

- Rotate cluster certificates
```bash
az aks rotate-certs --resource-group <resource-group> --name <cluster-name>
```

---

## Azure Container Registry (ACR) Integration

- Create Azure Container Registry
```bash
az acr create --resource-group <resource-group> --name <registry-name> --sku Basic
```

- Attach ACR to AKS cluster
```bash
az aks update \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --attach-acr <registry-name>
```

- Import image to ACR
```bash
az acr import \
  --name <registry-name> \
  --source docker.io/library/nginx:latest \
  --image nginx:latest
```

- List ACR repositories
```bash
az acr repository list --name <registry-name>
```

---

## Monitoring and Diagnostics

- Enable Azure Monitor for containers
```bash
az aks enable-addons \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --addons monitoring
```

- Get AKS cluster logs
```bash
az aks show --resource-group <resource-group> --name <cluster-name> --query "agentPoolProfiles[].diagnosticsProfile"
```

- Install kubectl if not available
```bash
az aks install-cli
```

- Check cluster health with kubectl
```bash
kubectl get nodes
kubectl get pods --all-namespaces
kubectl top nodes
kubectl top pods --all-namespaces
```

---

## Security and RBAC

- Enable RBAC on existing cluster
```bash
az aks update \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --enable-rbac
```

- Create AKS cluster with Azure AD integration
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --enable-aad \
  --aad-admin-group-object-ids <group-id>
```

- Get admin credentials (bypass RBAC)
```bash
az aks get-credentials \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --admin
```

- Create role binding for Azure AD user
```bash
kubectl create clusterrolebinding <binding-name> \
  --clusterrole=cluster-admin \
  --user=<user-email>
```

---

## Networking

- Enable HTTP application routing
```bash
az aks enable-addons \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --addons http_application_routing
```

- Get HTTP application routing zone name
```bash
az aks show \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --query "addonProfiles.httpApplicationRouting.config.HTTPApplicationRoutingZoneName"
```

- Create AKS cluster with load balancer SKU
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --load-balancer-sku standard
```

- Configure authorized IP ranges
```bash
az aks update \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --api-server-authorized-ip-ranges <ip-range>
```

---

## Storage

- Create Azure disk for persistent volume
```bash
az disk create \
  --resource-group <node-resource-group> \
  --name <disk-name> \
  --size-gb 20 \
  --sku Standard_LRS
```

- Create storage class for Azure Files
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: azurefile
provisioner: kubernetes.io/azure-file
parameters:
  skuName: Standard_LRS
  location: <region>
```

- Create persistent volume claim
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: azure-file-pvc
spec:
  accessModes:
    - ReadWriteMany
  storageClassName: azurefile
  resources:
    requests:
      storage: 5Gi
```

---

## Troubleshooting

- Get AKS cluster resource group
```bash
az aks show \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --query "nodeResourceGroup"
```

- View cluster events
```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
```

- Debug failed pods
```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name> --previous
```

- Check node conditions
```bash
kubectl describe nodes | grep -A 5 "Conditions:"
```

- SSH into AKS node (requires node access)
```bash
kubectl debug node/<node-name> -it --image=mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11
```

---

## PowerShell Commands

- Create AKS cluster with PowerShell
```powershell
New-AzAksCluster -ResourceGroupName <resource-group> -Name <cluster-name> -NodeCount 3 -GenerateSshKey
```

- Import AKS credentials with PowerShell
```powershell
Import-AzAksCredential -ResourceGroupName <resource-group> -Name <cluster-name>
```

- Scale node pool with PowerShell
```powershell
Set-AzAksCluster -ResourceGroupName <resource-group> -Name <cluster-name> -NodeCount 5
```

---

## Useful Aliases and Shortcuts

- Set up kubectl aliases
```bash
alias k='kubectl'
alias kgp='kubectl get pods'
alias kgs='kubectl get services'
alias kgn='kubectl get nodes'
alias kdp='kubectl describe pod'
alias kds='kubectl describe service'
```

- Quick cluster context switching
```bash
kubectl config get-contexts
kubectl config use-context <context-name>
```

- Port forward common services
```bash
kubectl port-forward service/kubernetes-dashboard 8443:443 -n kubernetes-dashboard
kubectl port-forward service/grafana 3000:80 -n monitoring
``` 