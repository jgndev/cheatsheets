---
id: 3
date: 2025-05-02T00:00:00Z
title: Kubectl Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for the kubectl command
slug: kubectl-cheatsheet
tags:
  - kubectl
published: true
---

# Kubectl Cheatsheet

---

## Configuration and Context Management

- Get current context
```bash
kubectl config current-context
```

- List all contexts
```bash
kubectl config get-contexts
```

- Switch to a different context
```bash
kubectl config use-context <context-name>
```

- Set default namespace for current context
```bash
kubectl config set-context --current --namespace=<namespace>
```

- View kubeconfig
```bash
kubectl config view
```

- Get cluster information
```bash
kubectl cluster-info
```

---

## Pod Management

- List all pods
```bash
kubectl get pods
```

- List pods in specific namespace
```bash
kubectl get pods -n <namespace>
```

- List pods with more details
```bash
kubectl get pods -o wide
```

- Create a pod from YAML file
```bash
kubectl apply -f <pod.yaml>
```

- Create a simple pod
```bash
kubectl run <pod-name> --image=<image-name>
```

- Delete a pod
```bash
kubectl delete pod <pod-name>
```

- Get pod details
```bash
kubectl describe pod <pod-name>
```

- Get pod logs
```bash
kubectl logs <pod-name>
```

- Follow pod logs
```bash
kubectl logs -f <pod-name>
```

- Execute commands in a pod
```bash
kubectl exec -it <pod-name> -- /bin/bash
```

---

## Deployment Management

- Create a deployment
```bash
kubectl create deployment <deployment-name> --image=<image-name>
```

- List all deployments
```bash
kubectl get deployments
```

- Get deployment details
```bash
kubectl describe deployment <deployment-name>
```

- Scale a deployment
```bash
kubectl scale deployment <deployment-name> --replicas=<number>
```

- Update deployment image
```bash
kubectl set image deployment/<deployment-name> <container-name>=<new-image>
```

- Rollback deployment
```bash
kubectl rollout undo deployment/<deployment-name>
```

- Check rollout status
```bash
kubectl rollout status deployment/<deployment-name>
```

- Delete a deployment
```bash
kubectl delete deployment <deployment-name>
```

---

## Service Management

- Create a service
```bash
kubectl expose deployment <deployment-name> --type=<service-type> --port=<port>
```

- List all services
```bash
kubectl get services
```

- Get service details
```bash
kubectl describe service <service-name>
```

- Delete a service
```bash
kubectl delete service <service-name>
```

- Port forward to a service
```bash
kubectl port-forward service/<service-name> <local-port>:<service-port>
```

---

## Namespace Management

- List all namespaces
```bash
kubectl get namespaces
```

- Create a namespace
```bash
kubectl create namespace <namespace-name>
```

- Delete a namespace
```bash
kubectl delete namespace <namespace-name>
```

- Get resources in all namespaces
```bash
kubectl get <resource-type> --all-namespaces
```

---

## ConfigMaps and Secrets

- Create ConfigMap from literal values
```bash
kubectl create configmap <configmap-name> --from-literal=<key>=<value>
```

- Create ConfigMap from file
```bash
kubectl create configmap <configmap-name> --from-file=<file-path>
```

- List ConfigMaps
```bash
kubectl get configmaps
```

- Create Secret from literal values
```bash
kubectl create secret generic <secret-name> --from-literal=<key>=<value>
```

- Create Secret from file
```bash
kubectl create secret generic <secret-name> --from-file=<file-path>
```

- List Secrets
```bash
kubectl get secrets
```

- Decode a secret
```bash
kubectl get secret <secret-name> -o jsonpath="{.data.<key>}" | base64 --decode
```

---

## Resource Inspection and Debugging

- Get all resources
```bash
kubectl get all
```

- Get resources with labels
```bash
kubectl get <resource-type> -l <label-key>=<label-value>
```

- Watch resource changes
```bash
kubectl get <resource-type> --watch
```

- Get resource in YAML format
```bash
kubectl get <resource-type> <resource-name> -o yaml
```

- Get resource in JSON format
```bash
kubectl get <resource-type> <resource-name> -o json
```

- Edit a resource
```bash
kubectl edit <resource-type> <resource-name>
```

- Get events
```bash
kubectl get events
```

- Get events sorted by timestamp
```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
```

---

## Node Management

- List all nodes
```bash
kubectl get nodes
```

- Get node details
```bash
kubectl describe node <node-name>
```

- Cordon a node (mark as unschedulable)
```bash
kubectl cordon <node-name>
```

- Uncordon a node
```bash
kubectl uncordon <node-name>
```

- Drain a node
```bash
kubectl drain <node-name> --ignore-daemonsets
```

---

## Persistent Volumes and Claims

- List Persistent Volumes
```bash
kubectl get pv
```

- List Persistent Volume Claims
```bash
kubectl get pvc
```

- Create PVC from file
```bash
kubectl apply -f <pvc.yaml>
```

- Delete PVC
```bash
kubectl delete pvc <pvc-name>
```

---

## Labels and Annotations

- Add label to resource
```bash
kubectl label <resource-type> <resource-name> <key>=<value>
```

- Remove label from resource
```bash
kubectl label <resource-type> <resource-name> <key>-
```

- Add annotation to resource
```bash
kubectl annotate <resource-type> <resource-name> <key>=<value>
```

- Remove annotation from resource
```bash
kubectl annotate <resource-type> <resource-name> <key>-
```

---

## Resource Management with Files

- Apply configuration from file
```bash
kubectl apply -f <file.yaml>
```

- Apply configurations from directory
```bash
kubectl apply -f <directory>/
```

- Apply with recursive directory search
```bash
kubectl apply -R -f <directory>/
```

- Delete resources from file
```bash
kubectl delete -f <file.yaml>
```

- Dry run before applying
```bash
kubectl apply -f <file.yaml> --dry-run=client
```

---

## Troubleshooting and Debugging

- Check resource usage of nodes
```bash
kubectl top nodes
```

- Check resource usage of pods
```bash
kubectl top pods
```

- Get pod logs from previous container instance
```bash
kubectl logs <pod-name> --previous
```

- Get logs from specific container in pod
```bash
kubectl logs <pod-name> -c <container-name>
```

- Copy files to/from pod
```bash
kubectl cp <pod-name>:<path> <local-path>
kubectl cp <local-path> <pod-name>:<path>
```

- Run debugging pod
```bash
kubectl run debug-pod --rm -i --tty --image=busybox -- /bin/sh
```

---

## Common Utilities

- Get kubectl version
```bash
kubectl version
```

- Get API resources
```bash
kubectl api-resources
```

- Get API versions
```bash
kubectl api-versions
```

- Explain resource fields
```bash
kubectl explain <resource-type>
```

- Explain specific field
```bash
kubectl explain <resource-type>.<field>
```

- Set output format
```bash
kubectl get <resource-type> -o wide
kubectl get <resource-type> -o yaml
kubectl get <resource-type> -o json
```

- Use custom columns
```bash
kubectl get pods -o custom-columns=NAME:.metadata.name,STATUS:.status.phase
```

- Get help for command
```bash
kubectl <command> --help
``` 