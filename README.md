# Container Migration in Kubernetes: Checkpointing, Restoration and Live Pod Transfer on AWS

This repository documents a complete Kubernetes experiment using AWS EKS to demonstrate live container migration using checkpointing and restoration. We deployed a scalable NGINX workload, collected real-time performance metrics, applied load, checkpointed an active pod, and successfully restored it on another node—all while the application was running!

---

## 🚀 Key Features

- ✅ AWS EKS cluster setup with 1 master and 10 worker nodes
- ✅ Scalable NGINX deployment across all nodes
- ✅ Metrics Server installed to monitor real-time resource utilization
- ✅ Applied HTTP load generation using the `hey` benchmarking tool
- ✅ Identified highest CPU/Memory-loaded pods and nodes dynamically
- ✅ Successfully checkpointed a running container using CRIU
- ✅ Restored the checkpoint on a different node using `nodeSelector`
- ✅ Captured migration metrics like response times, startup latency, and resource shifts
- ✅ Fully scripted and documented for reproducibility

---

## 🛠️ Setup Steps

### 1. 🌐 Create EKS Cluster (10 Worker Nodes)

```bash
eksctl create cluster --name research-cluster --region ap-south-1 --nodes 10

Verify node count:
kubectl get nodes

2. 📦 Deploy NGINX Across Cluster
kubectl create deployment nginx --image=nginx
kubectl scale deployment nginx --replicas=10
kubectl expose deployment nginx --name=nginx-service --port=80 --type=LoadBalancer
kubectl get svc nginx-service

✅ The last command gives you a public ELB URL like:
http://<external-load-balancer-dns>

3. 📈 Load Testing with Hey

Install hey:
go install github.com/rakyll/hey@latest

Run load:
hey -n 10000 -c 100 http://<elb-dns>

Example Output:
Requests/sec: 1767.0384
Latency: p50=0.0430s, p95=0.0888s

4. 🔍 Real-time Resource Utilization (Metrics Server)

Install Metrics Server:
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

Check node/pod resource stats:
kubectl top nodes
kubectl top pods -A --sort-by=cpu
kubectl top pods -A --sort-by=memory

5. 🧠 Checkpoint & Restore Container Using CRIU

✅ Get the Container ID:
kubectl describe pod <nginx-pod-name> -n default | grep "Container ID"

✅ Enable checkpointing:
sudo setcap cap_checkpoint_restore+eip $(which criu)

✅ Dump container state:
sudo criu dump -t <PID> --images-dir /tmp/checkpoint_dir --leave-running --unprivileged

✅ Restore on another node via a pod YAML:
spec:
  nodeSelector:
    kubernetes.io/hostname: <target-node>

📊 Results Summary
Metric	Value
Migration time	                ~XX ms
Curl time before migration	    ~XX ms
Curl time after migration	      ~YY ms
Resource freed (source node)	  ~ZZ% CPU/RAM
✅ Live NGINX traffic was uninterrupted during migration!

📂 Repository Structure
├── manifests/        # Deployment and service YAML files
├── results/          # Load testing and migration outputs
├── report/           # Full doc/pdf for the experiment
└── README.md         # You're reading it now!

📘 Reference Paper

This experimental setup is inspired by the paper:
"Container Placement and Migration in Edge Computing: Concepts and Scheduling Models"
