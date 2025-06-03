# Google Kubernetes Engine (GKE) Cheatsheet

---

## Cluster Management

- Create a basic GKE cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --num-nodes=3
```

- Create GKE cluster with machine type
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --machine-type=e2-standard-4 \
  --num-nodes=3 \
  --disk-size=100GB
```

- Create autopilot cluster (serverless)
```bash
gcloud container clusters create-auto <cluster-name> \
  --region=<region>
```

- Create private cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --enable-private-nodes \
  --master-ipv4-cidr-block=172.16.0.0/28 \
  --enable-ip-alias
```

- List all clusters
```bash
gcloud container clusters list
```

- Get cluster details
```bash
gcloud container clusters describe <cluster-name> --zone=<zone>
```

- Get cluster credentials
```bash
gcloud container clusters get-credentials <cluster-name> --zone=<zone>
```

- Delete cluster
```bash
gcloud container clusters delete <cluster-name> --zone=<zone>
```

---

## Node Pool Management

- List node pools
```bash
gcloud container node-pools list --cluster=<cluster-name> --zone=<zone>
```

- Create additional node pool
```bash
gcloud container node-pools create <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --machine-type=e2-standard-2 \
  --num-nodes=2
```

- Create preemptible node pool
```bash
gcloud container node-pools create <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --preemptible \
  --machine-type=e2-standard-2 \
  --num-nodes=3
```

- Create spot node pool
```bash
gcloud container node-pools create <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --spot \
  --machine-type=e2-standard-2 \
  --num-nodes=3
```

- Enable autoscaling for node pool
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-autoscaling \
  --node-pool=<pool-name> \
  --min-nodes=1 \
  --max-nodes=10
```

- Resize node pool
```bash
gcloud container clusters resize <cluster-name> \
  --zone=<zone> \
  --node-pool=<pool-name> \
  --num-nodes=5
```

- Delete node pool
```bash
gcloud container node-pools delete <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone>
```

---

## Cluster Operations

- Upgrade cluster master
```bash
gcloud container clusters upgrade <cluster-name> \
  --zone=<zone> \
  --master
```

- Upgrade cluster nodes
```bash
gcloud container clusters upgrade <cluster-name> \
  --zone=<zone> \
  --node-pool=<pool-name>
```

- Get available versions
```bash
gcloud container get-server-config --zone=<zone>
```

- Update cluster
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-autorepair \
  --enable-autoupgrade
```

---

## Google Container Registry (GCR) Integration

- Configure Docker for GCR
```bash
gcloud auth configure-docker
```

- Tag image for GCR
```bash
docker tag <image-name> gcr.io/<project-id>/<image-name>:<tag>
```

- Push image to GCR
```bash
docker push gcr.io/<project-id>/<image-name>:<tag>
```

- List images in GCR
```bash
gcloud container images list
```

- List tags for specific image
```bash
gcloud container images list-tags gcr.io/<project-id>/<image-name>
```

- Delete image from GCR
```bash
gcloud container images delete gcr.io/<project-id>/<image-name>:<tag>
```

---

## Networking

- Create cluster with custom network
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --network=<vpc-name> \
  --subnetwork=<subnet-name> \
  --enable-ip-alias
```

- Enable HTTP load balancing
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-http-load-balancing
```

- Enable network policy
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-network-policy
```

- Create cluster with authorized networks
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --enable-master-authorized-networks \
  --master-authorized-networks=<cidr-range>
```

---

## Security and Identity

- Enable Workload Identity
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --workload-pool=<project-id>.svc.id.goog
```

- Create service account for Workload Identity
```bash
gcloud iam service-accounts create <ksa-name>
```

- Bind Kubernetes SA to Google SA
```bash
gcloud iam service-accounts add-iam-policy-binding \
  --role roles/iam.workloadIdentityUser \
  --member "serviceAccount:<project-id>.svc.id.goog[<namespace>/<ksa-name>]" \
  <gsa-name>@<project-id>.iam.gserviceaccount.com
```

- Enable Binary Authorization
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-binauthz
```

- Enable Pod Security Policy
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-pod-security-policy
```

---

## Storage

- Create persistent disk
```bash
gcloud compute disks create <disk-name> \
  --size=10GB \
  --zone=<zone>
```

- Example StorageClass for SSD persistent disks
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: fast-ssd
provisioner: kubernetes.io/gce-pd
parameters:
  type: pd-ssd
  replication-type: none
```

- Example PVC using custom StorageClass
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: fast-storage
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: fast-ssd
  resources:
    requests:
      storage: 10Gi
```

---

## Monitoring and Logging

- Enable Cloud Monitoring
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-cloud-monitoring
```

- Enable Cloud Logging
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-cloud-logging
```

- View cluster operations
```bash
gcloud container operations list
```

- Describe specific operation
```bash
gcloud container operations describe <operation-id> --zone=<zone>
```

---

## Autopilot Clusters

- Create Autopilot cluster
```bash
gcloud container clusters create-auto <cluster-name> \
  --region=<region>
```

- Update Autopilot cluster
```bash
gcloud container clusters update <cluster-name> \
  --region=<region> \
  --enable-autoscaling
```

- Get Autopilot cluster info
```bash
gcloud container clusters describe <cluster-name> \
  --region=<region> \
  --format="value(autopilot)"
```

---

## Troubleshooting

- Check cluster status
```bash
gcloud container clusters describe <cluster-name> \
  --zone=<zone> \
  --format="value(status)"
```

- View cluster events
```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
```

- Check node status
```bash
kubectl get nodes -o wide
kubectl describe nodes
```

- Debug networking issues
```bash
kubectl run test-pod --image=busybox -it --rm -- nslookup kubernetes.default
```

- Check GKE add-ons status
```bash
gcloud container clusters describe <cluster-name> \
  --zone=<zone> \
  --format="value(addonsConfig)"
```

---

## Multi-Zone and Regional Clusters

- Create regional cluster
```bash
gcloud container clusters create <cluster-name> \
  --region=<region> \
  --num-nodes=1
```

- Create multi-zone cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --additional-zones=<zone1>,<zone2> \
  --num-nodes=1
```

- Add zones to existing cluster
```bash
gcloud container node-pools update <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --additional-zones=<zone1>,<zone2>
```

---

## Advanced Features

- Enable Istio service mesh
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-istio
```

- Enable cluster autoscaling
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-autoscaling \
  --min-nodes=1 \
  --max-nodes=10
```

- Enable vertical pod autoscaling
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-vertical-pod-autoscaling
```

- Enable shielded nodes
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-shielded-nodes
```

---

## Cost Optimization

- Create preemptible cluster
```bash
gcloud container clusters create <cluster-name> \
  --zone=<zone> \
  --preemptible \
  --num-nodes=3
```

- Enable cluster autoscaling
```bash
gcloud container clusters update <cluster-name> \
  --zone=<zone> \
  --enable-autoscaling \
  --min-nodes=0 \
  --max-nodes=5
```

- Use spot instances
```bash
gcloud container node-pools create <pool-name> \
  --cluster=<cluster-name> \
  --zone=<zone> \
  --spot \
  --num-nodes=3
```

---

## Useful kubectl Commands for GKE

- Check GKE cluster info
```bash
kubectl cluster-info
kubectl get nodes -o wide
kubectl get pods --all-namespaces
```

- Deploy from GCR
```bash
kubectl create deployment nginx --image=gcr.io/<project-id>/nginx:latest
```

- Create load balancer service
```bash
kubectl expose deployment nginx --port=80 --type=LoadBalancer
```

- Check GKE-specific annotations
```bash
kubectl get service nginx -o yaml | grep -A 5 -B 5 "cloud.google.com"
```

---

## Configuration Examples

- Example cluster with advanced features
```bash
gcloud container clusters create production-cluster \
  --zone=us-central1-a \
  --machine-type=e2-standard-4 \
  --num-nodes=3 \
  --enable-autoscaling \
  --min-nodes=1 \
  --max-nodes=10 \
  --enable-autorepair \
  --enable-autoupgrade \
  --enable-network-policy \
  --enable-ip-alias \
  --enable-cloud-logging \
  --enable-cloud-monitoring \
  --disk-size=100GB \
  --disk-type=pd-ssd
```

- Example Autopilot cluster
```bash
gcloud container clusters create-auto autopilot-cluster \
  --region=us-central1 \
  --enable-private-nodes \
  --enable-master-authorized-networks \
  --master-authorized-networks=10.0.0.0/8
``` 