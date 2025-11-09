# 📸 Screenshots – Kubernetes Container Migration Project

This folder contains visual evidence of the full workflow: cluster setup, deployment, monitoring, load testing, checkpointing, and post-migration validation.

---

## 1️⃣ Cluster Setup & Pod Deployment

### ✅ Nodes and Pods Running
![Cluster Nodes & Pods](Screenshots/kubectl-get-nodes-pods.png)

### ✅ Kubernetes Dashboard – Pod Overview
![Dashboard Pods](Screenshots/kubernetes-dashboard-pods.png)

---

## 2️⃣ Deployment Verification & YAML Export

### 📝 Deployment YAML Output
![Deployment YAML](Screenshots/kubectl-get-deployment-yaml.png)

### 📊 Dashboard – Workload Status
![Dashboard Workload](Screenshots/kubernetes-dashboard-workload-status.png)

---

## 3️⃣ Load Testing Before Migration

### ⚡ Load Test Results (`hey`)
![Load Test](Screenshots/hey-load-test-results.png)

---

## 4️⃣ Identifying Highest-Loaded Node/Pod

### 🔍 Resource Usage (kubectl top)
![Metrics Server Output](Screenshots/metrics-server-top-output.png)

### 📈 Sorted Nodes by CPU/Memory
![Top Nodes Sorted](Screenshots/kubectl-top-nodes-sort.png)

---

## 5️⃣ Migration Prep & Checkpointing

### 🎯 Selected Highest-Load Pod
![Target Pod](Screenshots/pod-identification-highest-load.png)

### 🗑️ Pod Deleted + Checkpoint Applied
![Checkpoint Apply](Screenshots/kubectl-delete-and-checkpoint-apply.png)

---

## 6️⃣ Post-Migration Validation

### ✅ Pod Successfully Restored on New Node
![Post-Migration Pods](Screenshots/post-migration-pods-list.png)

### 📉 Resource Usage After Migration
![Metrics After Migration](Screenshots/kubectl-top-after-migration.png)

---

## 🔁 Before vs After Comparison

| View | Screenshot |
|-------|------------|
| Before Migration Usage | ![Before Migration](Screenshots/kubectl-top-before-migration.png) |
| Top CPU Pods | ![Top CPU](Screenshots/kubectl-pod-top-cpu.png) |
| Top Memory Pods | ![Top Memory](Screenshots/kubectl-pod-top-memory.png) |

---

📌 **Note:** All screenshots are real outputs from AWS EKS cluster during live experiment.

