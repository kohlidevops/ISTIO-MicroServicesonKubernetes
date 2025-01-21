# To Install ISTIO on Kubernetes Cluster

## Pre-req

SSH to master node

```
sudo -i
kubectl get nodes
```

Install Kops on K8 master node

```
curl -Lo kops https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops
sudo mv kops /usr/local/bin/kops
```

Create a S3 bucket named "kops-latchu-bucket-a87654"

## Install Istio on Kubernetes Cluster

1. Deploy the Cluser with Medium Machine as Istio need memory to
start and work.

```
kops create cluster --state="s3://kops-latchu-bucket-a87654" --zones="ap-south-1a,ap-south-1b" --node-size=t2.medium --control-plane-size=t2.micro --control-plane-count 1 --node-count 2 --authorization=RBAC -- name=level360degree.uk --yes
```

![image](https://github.com/user-attachments/assets/e72cd987-2375-4e59-946a-d9d5130a2e65)

2. Validate Cluster is Running

```
kops validate cluster --state=s3://kops-latchu-bucket-a87654
```





