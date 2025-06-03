---
id: 8
date: 2025-05-02T00:00:00Z
title: Azure CLI Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for the Azure CLI
slug: az-cli-cheatsheet
tags:
  - azure
  - cli
published: true
---

# Azure CLI Cheatsheet

---

## Authentication and Account Management

- Login to Azure
```bash
az login
```

- Login with service principal
```bash
az login --service-principal -u <client-id> -p <client-secret> --tenant <tenant-id>
```

- Show current account information
```bash
az account show
```

- List available subscriptions
```bash
az account list
```

- Set active subscription
```bash
az account set --subscription <subscription-id>
```

- Logout from Azure
```bash
az logout
```

---

## Resource Groups

- Create a resource group
```bash
az group create --name <resource-group> --location <location>
```

- List all resource groups
```bash
az group list
```

- Show resource group details
```bash
az group show --name <resource-group>
```

- Delete a resource group
```bash
az group delete --name <resource-group> --yes --no-wait
```

- List resources in a resource group
```bash
az resource list --resource-group <resource-group>
```

---

## Virtual Machines

- Create a VM
```bash
az vm create \
  --resource-group <resource-group> \
  --name <vm-name> \
  --image <image> \
  --admin-username <username> \
  --generate-ssh-keys
```

- List all VMs
```bash
az vm list
```

- List VMs in a resource group
```bash
az vm list --resource-group <resource-group>
```

- Start a VM
```bash
az vm start --resource-group <resource-group> --name <vm-name>
```

- Stop a VM
```bash
az vm stop --resource-group <resource-group> --name <vm-name>
```

- Restart a VM
```bash
az vm restart --resource-group <resource-group> --name <vm-name>
```

- Delete a VM
```bash
az vm delete --resource-group <resource-group> --name <vm-name> --yes
```

- Show VM details
```bash
az vm show --resource-group <resource-group> --name <vm-name>
```

---

## Storage Accounts

- Create a storage account
```bash
az storage account create \
  --name <storage-account> \
  --resource-group <resource-group> \
  --location <location> \
  --sku Standard_LRS
```

- List storage accounts
```bash
az storage account list
```

- Show storage account details
```bash
az storage account show --name <storage-account> --resource-group <resource-group>
```

- Get storage account keys
```bash
az storage account keys list --account-name <storage-account> --resource-group <resource-group>
```

- Delete a storage account
```bash
az storage account delete --name <storage-account> --resource-group <resource-group> --yes
```

---

## App Services

- Create an App Service plan
```bash
az appservice plan create \
  --name <plan-name> \
  --resource-group <resource-group> \
  --sku B1
```

- Create a web app
```bash
az webapp create \
  --name <app-name> \
  --resource-group <resource-group> \
  --plan <plan-name>
```

- List web apps
```bash
az webapp list
```

- Deploy code to web app
```bash
az webapp deployment source config \
  --name <app-name> \
  --resource-group <resource-group> \
  --repo-url <git-repo-url> \
  --branch main
```

- Show web app details
```bash
az webapp show --name <app-name> --resource-group <resource-group>
```

- Delete a web app
```bash
az webapp delete --name <app-name> --resource-group <resource-group>
```

---

## Azure Container Instances (ACI)

- Create a container instance
```bash
az container create \
  --resource-group <resource-group> \
  --name <container-name> \
  --image <image> \
  --ports 80
```

- List container instances
```bash
az container list
```

- Show container logs
```bash
az container logs --resource-group <resource-group> --name <container-name>
```

- Delete a container instance
```bash
az container delete --resource-group <resource-group> --name <container-name> --yes
```

---

## Azure Kubernetes Service (AKS)

- Create an AKS cluster
```bash
az aks create \
  --resource-group <resource-group> \
  --name <cluster-name> \
  --node-count 1 \
  --enable-addons monitoring \
  --generate-ssh-keys
```

- Get AKS credentials
```bash
az aks get-credentials --resource-group <resource-group> --name <cluster-name>
```

- List AKS clusters
```bash
az aks list
```

- Scale AKS cluster
```bash
az aks scale --resource-group <resource-group> --name <cluster-name> --node-count 3
```

- Delete AKS cluster
```bash
az aks delete --resource-group <resource-group> --name <cluster-name> --yes
```

---

## Networking

- Create a virtual network
```bash
az network vnet create \
  --resource-group <resource-group> \
  --name <vnet-name> \
  --subnet-name <subnet-name>
```

- Create a network security group
```bash
az network nsg create \
  --resource-group <resource-group> \
  --name <nsg-name>
```

- Create a public IP
```bash
az network public-ip create \
  --resource-group <resource-group> \
  --name <public-ip-name>
```

- List virtual networks
```bash
az network vnet list
```

---

## Key Vault

- Create a key vault
```bash
az keyvault create \
  --name <keyvault-name> \
  --resource-group <resource-group> \
  --location <location>
```

- Set a secret
```bash
az keyvault secret set \
  --vault-name <keyvault-name> \
  --name <secret-name> \
  --value <secret-value>
```

- Get a secret
```bash
az keyvault secret show \
  --vault-name <keyvault-name> \
  --name <secret-name>
```

- List secrets
```bash
az keyvault secret list --vault-name <keyvault-name>
```

---

## Monitoring and Diagnostics

- Get activity logs
```bash
az monitor activity-log list --resource-group <resource-group>
```

- Create an alert rule
```bash
az monitor metrics alert create \
  --name <alert-name> \
  --resource-group <resource-group> \
  --scopes <resource-id> \
  --condition "avg Percentage CPU > 80"
```

- List available metrics
```bash
az monitor metrics list-definitions --resource <resource-id>
```

---

## Common Utilities

- Show CLI version
```bash
az version
```

- Update Azure CLI
```bash
az upgrade
```

- Get help for a command
```bash
az <command> --help
```

- Set output format (json, table, tsv)
```bash
az configure --defaults output=table
```

- Enable CLI extensions
```bash
az extension add --name <extension-name>
```

- List installed extensions
```bash
az extension list
``` 