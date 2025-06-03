---
id: 6
date: 2025-05-02T00:00:00Z
title: Gcloud Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for the gcloud command
slug: gcloud-cheatsheet
tags:
  - gcloud
  - gcp
published: true
---

# Google Cloud CLI (gcloud) Cheatsheet

---

## Authentication and Configuration

- Login to Google Cloud
```bash
gcloud auth login
```

- Login with service account
```bash
gcloud auth activate-service-account --key-file=<key-file.json>
```

- List authenticated accounts
```bash
gcloud auth list
```

- Set default project
```bash
gcloud config set project <project-id>
```

- Get current project
```bash
gcloud config get-value project
```

- Set default region
```bash
gcloud config set compute/region <region>
```

- Set default zone
```bash
gcloud config set compute/zone <zone>
```

- List all configurations
```bash
gcloud config list
```

- Create new configuration
```bash
gcloud config configurations create <config-name>
```

- Switch configuration
```bash
gcloud config configurations activate <config-name>
```

---

## Project Management

- List all projects
```bash
gcloud projects list
```

- Create a new project
```bash
gcloud projects create <project-id> --name="<project-name>"
```

- Delete a project
```bash
gcloud projects delete <project-id>
```

- Get project information
```bash
gcloud projects describe <project-id>
```

- Enable API service
```bash
gcloud services enable <service-name>
```

- List enabled services
```bash
gcloud services list --enabled
```

---

## Compute Engine

- List all VM instances
```bash
gcloud compute instances list
```

- Create a VM instance
```bash
gcloud compute instances create <instance-name> \
  --zone=<zone> \
  --machine-type=<machine-type> \
  --image-family=<image-family> \
  --image-project=<image-project>
```

- Start a VM instance
```bash
gcloud compute instances start <instance-name> --zone=<zone>
```

- Stop a VM instance
```bash
gcloud compute instances stop <instance-name> --zone=<zone>
```

- Delete a VM instance
```bash
gcloud compute instances delete <instance-name> --zone=<zone>
```

- SSH into VM instance
```bash
gcloud compute ssh <instance-name> --zone=<zone>
```

- Get VM instance details
```bash
gcloud compute instances describe <instance-name> --zone=<zone>
```

- List machine types
```bash
gcloud compute machine-types list --zones=<zone>
```

- List available images
```bash
gcloud compute images list
```

---

## Cloud Storage

- List all buckets
```bash
gcloud storage buckets list
```

- Create a bucket
```bash
gcloud storage buckets create gs://<bucket-name>
```

- Delete a bucket
```bash
gcloud storage buckets delete gs://<bucket-name>
```

- Upload file to bucket
```bash
gcloud storage cp <local-file> gs://<bucket-name>/
```

- Download file from bucket
```bash
gcloud storage cp gs://<bucket-name>/<file> <local-path>
```

- Sync directory with bucket
```bash
gcloud storage rsync <local-directory> gs://<bucket-name>
```

- List objects in bucket
```bash
gcloud storage ls gs://<bucket-name>
```

- Make bucket public
```bash
gcloud storage buckets add-iam-policy-binding gs://<bucket-name> \
  --member="allUsers" --role="roles/storage.objectViewer"
```

---

## Google Kubernetes Engine (GKE)

- List GKE clusters
```bash
gcloud container clusters list
```

- Create a GKE cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --num-nodes=<node-count>
```

- Get cluster credentials
```bash
gcloud container clusters get-credentials <cluster-name> --zone=<zone>
```

- Resize cluster
```bash
gcloud container clusters resize <cluster-name> --num-nodes=<node-count> --zone=<zone>
```

- Delete GKE cluster
```bash
gcloud container clusters delete <cluster-name> --zone=<zone>
```

- List node pools
```bash
gcloud container node-pools list --cluster=<cluster-name> --zone=<zone>
```

- Create node pool
```bash
gcloud container node-pools create <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --num-nodes=<node-count>
```

---

## App Engine

- Deploy application
```bash
gcloud app deploy
```

- Browse deployed application
```bash
gcloud app browse
```

- View application logs
```bash
gcloud app logs tail -s default
```

- List versions
```bash
gcloud app versions list
```

- Set traffic allocation
```bash
gcloud app services set-traffic --splits=<version>=<traffic-percentage>
```

- Delete version
```bash
gcloud app versions delete <version>
```

---

## Cloud Functions

- List all functions
```bash
gcloud functions list
```

- Deploy a function
```bash
gcloud functions deploy <function-name> \
  --runtime=<runtime> \
  --trigger-http \
  --source=<source-path>
```

- Call a function
```bash
gcloud functions call <function-name>
```

- Get function details
```bash
gcloud functions describe <function-name>
```

- View function logs
```bash
gcloud functions logs read <function-name>
```

- Delete a function
```bash
gcloud functions delete <function-name>
```

---

## Identity and Access Management (IAM)

- List IAM policies
```bash
gcloud projects get-iam-policy <project-id>
```

- Add IAM policy binding
```bash
gcloud projects add-iam-policy-binding <project-id> \
  --member="user:<email>" \
  --role="<role>"
```

- Remove IAM policy binding
```bash
gcloud projects remove-iam-policy-binding <project-id> \
  --member="user:<email>" \
  --role="<role>"
```

- List service accounts
```bash
gcloud iam service-accounts list
```

- Create service account
```bash
gcloud iam service-accounts create <account-name> \
  --display-name="<display-name>"
```

- Create service account key
```bash
gcloud iam service-accounts keys create <key-file.json> \
  --iam-account=<service-account-email>
```

- List IAM roles
```bash
gcloud iam roles list
```

---

## Networking

- List VPC networks
```bash
gcloud compute networks list
```

- Create VPC network
```bash
gcloud compute networks create <network-name> --subnet-mode=<mode>
```

- List subnets
```bash
gcloud compute networks subnets list
```

- Create subnet
```bash
gcloud compute networks subnets create <subnet-name> \
  --network=<network-name> \
  --range=<cidr-range> \
  --region=<region>
```

- List firewall rules
```bash
gcloud compute firewall-rules list
```

- Create firewall rule
```bash
gcloud compute firewall-rules create <rule-name> \
  --allow=<protocol>:<port> \
  --source-ranges=<cidr>
```

- List static IP addresses
```bash
gcloud compute addresses list
```

- Reserve static IP
```bash
gcloud compute addresses create <address-name> --region=<region>
```

---

## Cloud SQL

- List SQL instances
```bash
gcloud sql instances list
```

- Create SQL instance
```bash
gcloud sql instances create <instance-name> \
  --database-version=<version> \
  --tier=<tier> \
  --region=<region>
```

- Connect to SQL instance
```bash
gcloud sql connect <instance-name> --user=<username>
```

- Create database
```bash
gcloud sql databases create <database-name> --instance=<instance-name>
```

- List databases
```bash
gcloud sql databases list --instance=<instance-name>
```

- Export database
```bash
gcloud sql export sql <instance-name> gs://<bucket-name>/<file-name> \
  --database=<database-name>
```

---

## Monitoring and Logging

- View logs
```bash
gcloud logging read "resource.type=<resource-type>"
```

- List log entries
```bash
gcloud logging entries list --filter="<filter>"
```

- Create log-based metric
```bash
gcloud logging metrics create <metric-name> --description="<description>" \
  --log-filter="<filter>"
```

- List monitoring metrics
```bash
gcloud monitoring metrics list
```

- Create alerting policy
```bash
gcloud alpha monitoring policies create --policy-from-file=<policy-file.yaml>
```

---

## Billing and Quotas

- List billing accounts
```bash
gcloud billing accounts list
```

- Link project to billing account
```bash
gcloud billing projects link <project-id> --billing-account=<account-id>
```

- List quotas
```bash
gcloud compute project-info describe --format="table(quotas[].metric,quotas[].limit,quotas[].usage)"
```

- List regions and zones
```bash
gcloud compute regions list
gcloud compute zones list
```

---

## Common Utilities

- Get gcloud version
```bash
gcloud version
```

- Update gcloud components
```bash
gcloud components update
```

- Install additional components
```bash
gcloud components install <component-name>
```

- List installed components
```bash
gcloud components list
```

- Get help for command
```bash
gcloud <command> --help
```

- Set output format
```bash
gcloud config set core/format <format>
```

- Enable/disable command completion
```bash
gcloud info --show-log
```

- Clear cache
```bash
gcloud config configurations list
```

- Show current configuration
```bash
gcloud info
``` 