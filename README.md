# k8s-nfs-deployment

## Prerequisites

- Kubernetes Cluster (can be set up with KIND or Minikube)
- Helm (for installation of NFS provisioner)
- Docker (for KIND)

## Setup

1. **Add Helm repo for NFS Provisioner:**

```bash
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm repo update

2. **Install NFS Ganesha Provisioner**

```bash
helm install my-release nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner --set image.repository=k8s.gcr.io/sig-storage/nfs-provisioner --set image.tag=v3.0.0 --set storageClass.name=my-custom-storage-class
```

3. **Apply the PVC, Deployment, Service, and Job:**

```bash
kubectl apply -f nfs-pvc.yaml
kubectl apply -f nginx-nfs-deploy.yaml
kubectl apply -f nginx-nfs-service.yaml
kubectl apply -f nfs-content-loader-job.
```

4. **Acess the nginx server**
```bash
kubectl port-forward service/nginx-nfs 8080:80
curl http://localhost:8080
```
Or simply go to http://localhost:8080 in the browser (if using kind port-forward is required)
