---
id: 7
date: 2025-05-02T00:00:00Z
title: Azure PowerShell Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for Azure PowerShell
slug: az-powershell-cheatsheet
tags:
  - azure
  - powershell
published: true
---

# Azure PowerShell Cheatsheet

---

## Installation and Authentication

- Install Azure PowerShell module
```powershell
Install-Module -Name Az -Repository PSGallery -Force
```

- Update Azure PowerShell module
```powershell
Update-Module -Name Az
```

- Login to Azure
```powershell
Connect-AzAccount
```

- Login with service principal
```powershell
$credential = Get-Credential
Connect-AzAccount -ServicePrincipal -Credential $credential -Tenant <tenant-id>
```

- Show current context
```powershell
Get-AzContext
```

- List available subscriptions
```powershell
Get-AzSubscription
```

- Set active subscription
```powershell
Set-AzContext -SubscriptionId <subscription-id>
```

- Disconnect from Azure
```powershell
Disconnect-AzAccount
```

---

## Resource Groups

- Create a resource group
```powershell
New-AzResourceGroup -Name <resource-group> -Location <location>
```

- Get all resource groups
```powershell
Get-AzResourceGroup
```

- Get specific resource group
```powershell
Get-AzResourceGroup -Name <resource-group>
```

- Remove a resource group
```powershell
Remove-AzResourceGroup -Name <resource-group> -Force
```

- Get resources in a resource group
```powershell
Get-AzResource -ResourceGroupName <resource-group>
```

---

## Virtual Machines

- Create a VM
```powershell
$vm = New-AzVMConfig -VMName <vm-name> -VMSize "Standard_B2s"
$vm = Set-AzVMOperatingSystem -VM $vm -Windows -ComputerName <vm-name> -Credential $credential
$vm = Set-AzVMSourceImage -VM $vm -PublisherName "MicrosoftWindowsServer" -Offer "WindowsServer" -Skus "2019-Datacenter" -Version "latest"
New-AzVM -ResourceGroupName <resource-group> -Location <location> -VM $vm
```

- Get all VMs
```powershell
Get-AzVM
```

- Get VMs in a resource group
```powershell
Get-AzVM -ResourceGroupName <resource-group>
```

- Start a VM
```powershell
Start-AzVM -ResourceGroupName <resource-group> -Name <vm-name>
```

- Stop a VM
```powershell
Stop-AzVM -ResourceGroupName <resource-group> -Name <vm-name> -Force
```

- Restart a VM
```powershell
Restart-AzVM -ResourceGroupName <resource-group> -Name <vm-name>
```

- Remove a VM
```powershell
Remove-AzVM -ResourceGroupName <resource-group> -Name <vm-name> -Force
```

- Get VM status
```powershell
Get-AzVM -ResourceGroupName <resource-group> -Name <vm-name> -Status
```

---

## Storage Accounts

- Create a storage account
```powershell
New-AzStorageAccount -ResourceGroupName <resource-group> -Name <storage-account> -Location <location> -SkuName "Standard_LRS"
```

- Get all storage accounts
```powershell
Get-AzStorageAccount
```

- Get specific storage account
```powershell
Get-AzStorageAccount -ResourceGroupName <resource-group> -Name <storage-account>
```

- Get storage account keys
```powershell
Get-AzStorageAccountKey -ResourceGroupName <resource-group> -Name <storage-account>
```

- Remove a storage account
```powershell
Remove-AzStorageAccount -ResourceGroupName <resource-group> -Name <storage-account> -Force
```

---

## App Services

- Create an App Service plan
```powershell
New-AzAppServicePlan -ResourceGroupName <resource-group> -Name <plan-name> -Location <location> -Tier "Basic" -NumberofWorkers 1 -WorkerSize "Small"
```

- Create a web app
```powershell
New-AzWebApp -ResourceGroupName <resource-group> -Name <app-name> -Location <location> -AppServicePlan <plan-name>
```

- Get all web apps
```powershell
Get-AzWebApp
```

- Get web app details
```powershell
Get-AzWebApp -ResourceGroupName <resource-group> -Name <app-name>
```

- Remove a web app
```powershell
Remove-AzWebApp -ResourceGroupName <resource-group> -Name <app-name> -Force
```

---

## Azure Container Instances (ACI)

- Create a container group
```powershell
New-AzContainerGroup -ResourceGroupName <resource-group> -Name <container-name> -Image <image> -OsType Linux -Port 80
```

- Get container groups
```powershell
Get-AzContainerGroup
```

- Get container logs
```powershell
Get-AzContainerInstanceLog -ResourceGroupName <resource-group> -ContainerGroupName <container-name>
```

- Remove a container group
```powershell
Remove-AzContainerGroup -ResourceGroupName <resource-group> -Name <container-name>
```

---

## Azure Kubernetes Service (AKS)

- Create an AKS cluster
```powershell
New-AzAksCluster -ResourceGroupName <resource-group> -Name <cluster-name> -NodeCount 1 -GenerateSshKey
```

- Get AKS credentials
```powershell
Import-AzAksCredential -ResourceGroupName <resource-group> -Name <cluster-name>
```

- Get AKS clusters
```powershell
Get-AzAksCluster
```

- Remove AKS cluster
```powershell
Remove-AzAksCluster -ResourceGroupName <resource-group> -Name <cluster-name> -Force
```

---

## Networking

- Create a virtual network
```powershell
$subnet = New-AzVirtualNetworkSubnetConfig -Name <subnet-name> -AddressPrefix "10.0.1.0/24"
New-AzVirtualNetwork -ResourceGroupName <resource-group> -Location <location> -Name <vnet-name> -AddressPrefix "10.0.0.0/16" -Subnet $subnet
```

- Create a network security group
```powershell
New-AzNetworkSecurityGroup -ResourceGroupName <resource-group> -Location <location> -Name <nsg-name>
```

- Create a public IP
```powershell
New-AzPublicIpAddress -ResourceGroupName <resource-group> -Location <location> -Name <public-ip-name> -AllocationMethod Dynamic
```

- Get virtual networks
```powershell
Get-AzVirtualNetwork
```

---

## Key Vault

- Create a key vault
```powershell
New-AzKeyVault -ResourceGroupName <resource-group> -VaultName <keyvault-name> -Location <location>
```

- Set a secret
```powershell
$secret = ConvertTo-SecureString -String <secret-value> -AsPlainText -Force
Set-AzKeyVaultSecret -VaultName <keyvault-name> -Name <secret-name> -SecretValue $secret
```

- Get a secret
```powershell
Get-AzKeyVaultSecret -VaultName <keyvault-name> -Name <secret-name>
```

- List secrets
```powershell
Get-AzKeyVaultSecret -VaultName <keyvault-name>
```

---

## Monitoring and Diagnostics

- Get activity logs
```powershell
Get-AzLog -ResourceGroup <resource-group>
```

- Create an alert rule
```powershell
Add-AzMetricAlertRuleV2 -ResourceGroupName <resource-group> -Name <alert-name> -TargetResourceId <resource-id> -MetricName "Percentage CPU" -Operator GreaterThan -Threshold 80
```

- Get available metrics
```powershell
Get-AzMetricDefinition -ResourceId <resource-id>
```

---

## Role-Based Access Control (RBAC)

- Get role assignments
```powershell
Get-AzRoleAssignment -ResourceGroupName <resource-group>
```

- Create role assignment
```powershell
New-AzRoleAssignment -SignInName <user-email> -RoleDefinitionName "Contributor" -ResourceGroupName <resource-group>
```

- Remove role assignment
```powershell
Remove-AzRoleAssignment -SignInName <user-email> -RoleDefinitionName "Contributor" -ResourceGroupName <resource-group>
```

- Get role definitions
```powershell
Get-AzRoleDefinition
```

---

## Common Utilities

- Get Azure PowerShell version
```powershell
Get-Module -Name Az -ListAvailable
```

- Import specific Azure module
```powershell
Import-Module Az.Resources
```

- Get command help
```powershell
Get-Help <command-name> -Full
```

- Set default resource group
```powershell
Set-AzDefault -ResourceGroupName <resource-group>
```

- Clear Azure context
```powershell
Clear-AzContext
```

- Export Azure context
```powershell
Save-AzContext -Path "C:\AzureContext.json"
``` 